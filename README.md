# Laçamento de Aplicação
Recebi a responsabilidade de analisar os dados fornecidos para indicar o melhor horario e melhor sistema operacional para lançamento de uma nova aplicação pelo gestor.

as principais questões a serem respondidas para indicar o melhor horário e o melhor sistema foram as seguintes:

01 - ANALISE DE INTERAÇÕES DOS USUÁRIOS:

      select 
          hour(hour),
          count (hour) as 'Usuários Logados',
          sum(used_premium_feature) as 'Funcionalidades Premium Utilizadas',
          sum(liked) as 'Avaliações positivas'
      from
          interaction
      group by hour
      order by hour
      
02 - FATURAMENTO POR DIA:

      select sum (tax), day (date) from tax
      left join transactions on tax.transaction_id = transactions.transaction_id
      where day (date) between 23 and 29 -- filtron pela data
      group by day(date) -- agrupar por data
      order by day(date) -- ordenar por data

03 - FATURAMENTO POR PEÍODO:

    select sum (tax) from tax
    left join transactions on tax.transaction_id = transactions.transaction_id
    where day (date) between 23 and 29

04 - PROPORÇÃO DE USUÁRIOS:

    With Sistema as (
        select 
            case
                when ios_user = 1 then 'Usuário de IOS'
                when ios_user = 0 then 'Usuário de Android'
            end as 'Sistema_Operacional'
        from user
        where churn = 0
    )
    
    select
        Sistema_Operacional,
        count(Sistema_Operacional)
    from    
        Sistema
    group by Sistema_Operacional
