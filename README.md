# Criação de Login e Usuário no SQL Server com Permissões

Este conjunto de scripts SQL demonstra a criação de um login no nível do servidor SQL Server, a criação de um usuário de banco de dados associado e a atribuição de permissões.

<H3> Criação de Login SQL </H3>

> CREATE LOGIN [nome.usuario] WITH PASSWORD = 'senha@123' ;
 
<P>Este comando cria um novo login no servidor SQL Server com o nome nome.usuario e define a senha para senha@123. Este login é a credencial para acessar o servidor. 
<BR><STRONG>Importante:</STRONG> Em ambientes de produção, utilize senhas fortes e complexas. </P>

<H3>Criação de Usuário de Banco de Dados</H3>
 
CREATE USER [nome.usuario] FOR LOGIN [nome.usuario] WITH DEFAULT_SCHEMA = dbo;
Este comando cria um usuário dentro do banco de dados atual com o nome nome.usuario e o associa ao login criado anteriormente. O DEFAULT_SCHEMA = dbo define o schema padrão para os objetos criados por este usuário.

<H3> Verificação de Permissões </H3>
 
> SELECT
    roles.principal_id AS RolePrincipalID
    ,   roles.name AS RolePrincipalName
    ,   database_role_members.member_principal_id    AS MemberPrincipalID
    ,   members.name                                    AS MemberPrincipalName
<BR> FROM sys.database_role_members AS database_role_members
<BR> JOIN sys.database_principals AS roles
    ON database_role_members.role_principal_id = roles.principal_id
<BR>JOIN sys.database_principals AS members
    ON database_role_members.member_principal_id = members.principal_id;

<P> Esta consulta SQL busca informações das tabelas de sistema para listar os usuários do banco de dados e suas respectivas associações a roles de banco de dados. Isso permite verificar as permissões concedidas. </P>
 

<H3>Alteração de Permissão (Adição a Role) </H3>

> EXEC sp_addrolemember 'db_owner', 'usuario.02';

<P> Este comando executa o procedimento armazenado do sistema sp_addrolemember para adicionar o usuário de banco de dados usuario.02 à role de banco de dados fixa db_owner. A role db_owner concede controle total sobre o banco de dados.</P>

<H3>Próximo Passo: Query de Schema</H3>

> Query dbschema
<P> Esta instrução indica que o próximo passo seria executar uma consulta para visualizar o schema do banco de dados, utilizando comandos como SELECT * FROM INFORMATION_SCHEMA.TABLES; ou explorando as ferramentas de gerenciamento do SQL Server. </P> 
