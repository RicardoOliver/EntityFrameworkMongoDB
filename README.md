# EntityFrameworkMongoDB


```using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.EntityFrameworkCore;
using MongoDB.Driver;

namespace EntityFrameworkMongoDB
{
    public class Program
    {
        public static void Main(string[] args)
        {
            
            // Configurações de conexão com bancos de dados
            string sqlServerConnectionString = "sua-string-de-conexao-do-SQL-Server";
            string mongoDBConnectionString = "sua-string-de-conexao-do-MongoDB";

            // Exemplo de uso do Entity Framework (SQL Server)
            using (var dbContext = new DbContext(sqlServerConnectionString))
            {
                // Consulta utilizando LINQ
                var customers = dbContext.Customers.Where(c => c.IsActive).ToList();
                foreach (var customer in customers)
                {
                    Console.WriteLine(customer.Name);
                }
            }

            // Exemplo de uso do MongoDB
            var mongoClient = new MongoClient(mongoDBConnectionString);
            var mongoDatabase = mongoClient.GetDatabase("nome-do-banco-de-dados");

            var collection = mongoDatabase.GetCollection<YourEntity>("nome-da-colecao");
            var documents = collection.Find(Builders<YourEntity>.Filter.Empty).ToList();
            foreach (var document in documents)
            {
                Console.WriteLine(document.Name);
            }

            // Outras tarefas do desenvolvedor backend sênior, como integração com Azure DevOps, CI/CD, microserviços, TDD, DDD, Clean Code, etc.

            Console.ReadLine();
        }
    }

    // Exemplo de entidade para o MongoDB
    public class YourEntity
    {
        public string Id { get; set; }
        public string Name { get; set; }
        // Outros campos...
    }

    // Exemplo de entidade para o Entity Framework (SQL Server)
    public class Customer
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public bool IsActive { get; set; }
        // Outros campos...
    }

    // Exemplo de DbContext para o Entity Framework (SQL Server)
    public class DbContext : Microsoft.EntityFrameworkCore.DbContext
    {
        private readonly string _connectionString;

        public DbContext(string connectionString)
        {
            _connectionString = connectionString;
        }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseSqlServer(_connectionString);
        }

        public DbSet<Customer> Customers { get; set; }
        // Outros DbSets...
    }
}


O código fornecido é um exemplo básico de uma aplicação em C# que ilustra o uso do Entity Framework para acesso a um banco de dados SQL Server e do driver do MongoDB para acesso a um banco de dados MongoDB.[^1]
[^1]: 
