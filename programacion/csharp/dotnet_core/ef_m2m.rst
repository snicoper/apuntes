.. _reference-programacion-csharp-dotnet_core-ef-m2m:

#############
EF ManyToMany
#############

.. code-block:: csharp

    using System;
    using System.Collections.Generic;
    using System.ComponentModel.DataAnnotations.Schema;

    namespace Practica.Models
    {
        [Table("Tags")]
        public class Tag
        {
            public int Id { get; set; }
            public string Title { get; set; }
            public ICollection<TagArticle> TagArticles { get; set; }
        }

        [Table("Articles")]
        public class Article
        {
            public int Id { get; set; }
            public string Title { get; set; }
            public string Body { get; set; }
            public ICollection<TagArticle> TagArticles { get; set; }
        }

        public class TagArticle
        {
            public int TagId { get; set; }
            public Tag Tag { get; set; }
            public int ArticleId { get; set; }
            public Article Article { get; set; }
        }
    }

Editar el archivo de db context.

.. code-block:: csharp

    using Microsoft.EntityFrameworkCore;

    namespace Practica.Models
    {
        public class ApplicationDbContext : DbContext
        {
            public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options)
            {
            }

            public virtual DbSet<Tag> Tags { get; set; }
            public virtual DbSet<Article> Articles { get; set; }

            protected override void OnModelCreating(ModelBuilder modelBuilder)
            {
                // ManyToMany Tag/Article.
                modelBuilder.Entity<TagArticle>()
                    .HasKey(ta => new { ta.TagId, ta.ArticleId });

                modelBuilder.Entity<TagArticle>()
                    .HasOne(ta => ta.Tag)
                    .WithMany(t => t.TagArticles)
                    .HasForeignKey(ta => ta.TagId);

                modelBuilder.Entity<TagArticle>()
                    .HasOne(ta => ta.Article)
                    .WithMany(a => a.TagArticles)
                    .HasForeignKey(ta => ta.ArticleId);
            }
        }
    }
