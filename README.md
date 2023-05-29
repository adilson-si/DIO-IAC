# DIO-IAC

Este arquivo descreve um exemplo simples de modelo de infra estrutura como código usado no curso da DIO do Bootcamp de Cloud AWS


Sequência de eventos durante a implantação:

Antes de o aplicativo Amazon ECS atualizado ser instalado no conjunto de tarefas de substituição, a função Lambda chamada FuncaoLambdaToValidateBeforeInstall é executada.

Depois que o aplicativo Amazon ECS atualizado é instalado no conjunto de tarefas de substituição, mas antes de receber qualquer tráfego, a função Lambda chamada FuncaoLambdaToValidateAfterInstall é executada.

Depois que o aplicativo Amazon ECS no conjunto de tarefas de substituição começar a receber tráfego do ouvinte de teste, a função Lambda chamada FuncaoLambdaToValidateAfterTestTrafficStarts é executada. Essa função provavelmente executa testes de validação para determinar se a implantação continua. Se você não especificar um listener de teste no seu grupo de implantação, este gancho será ignorado.

Depois que qualquer teste de validação noAfterAllowTestTraffic gancho for concluído e antes que o tráfego de produção seja fornecido ao aplicativo Amazon ECS atualizado, a função Lambda chamada FuncaoLambdaToValidateBeforeAllowingProductionTraffic é executada.

Depois que o tráfego de produção é enviado para o aplicativo Amazon ECS atualizado no conjunto de tarefas de substituição, a função Lambda chamada FuncaoLambdaToValidateAfterAllowingProductionTraffic é executada.

As funções do Lambda que são executadas durante qualquer gancho podem realizar testes de validação ou coletar métricas de tráfego.
