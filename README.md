
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace ArticleInfo
{
    public partial class Form1 : Form
    {
        // список для збереження статей
        private List<Article> articles = new List<Article>();

        public Form1()
        {
            InitializeComponent();
        }

        // клас для однієї статті
        public class Article
        {
            private string author;
            private int pages;

            public string Title { get; set; }
            public string Topic { get; set; }
            public string PublishDate { get; set; }
            public string Place { get; set; }

            // Методи доступу до приватних полів
            public void SetAuthor(string value)
            {
                author = value;
            }

            public string GetAuthor()
            {
                return author;
            }

            public void SetPages(int value)
            {
                if (value > 0)
                    pages = value;
            }

            public int GetPages()
            {
                return pages;
            }

            // Перевизначення ToString()
            public override string ToString()
            {
                return $"Автор: {author}\n" +
                       $"Кількість сторінок: {pages}\n" +
                       $"Назва: {Title}\n" +
                       $"Тема: {Topic}\n" +
                       $"Дата публікації: {PublishDate}\n" +
                       $"Місце: {Place}\n";
            }
        }

        // кнопка "Ввести"
        private void btnInput_Click(object sender, EventArgs e)
        {
            try
            {
                Article article = new Article();
                article.SetAuthor(txtAuthor.Text);
                article.SetPages(int.Parse(txtPages.Text));
                article.Title = txtTitle.Text;
                article.Topic = txtTopic.Text;
                article.PublishDate = txtDate.Text;
                article.Place = txtPlace.Text;

                articles.Add(article);

                // очищення полів
                txtAuthor.Clear();
                txtPages.Clear();
                txtTitle.Clear();
                txtTopic.Clear();
                txtDate.Clear();
                txtPlace.Clear();

                MessageBox.Show("Статтю додано!");
            }
            catch
            {
                MessageBox.Show("Помилка введення даних!");
            }
        }

        // кнопка "Вивести"
        private void btnOutput_Click(object sender, EventArgs e)
        {
            if (articles.Count == 0)
            {
                MessageBox.Show("Немає збережених статей!");
                return;
            }

            string result = "";
            foreach (var a in articles)
            {
                result += a.ToString() + "-------------------------\n";
            }

            MessageBox.Show(result, "Список статей");
        }
    }
}
