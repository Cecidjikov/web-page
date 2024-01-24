using System;

// Клас, представляващ уеб страница
public class WebPage
{
    public string Title { get; set; }
    public string Header { get; set; }
    public string Content { get; set; }
    public string Footer { get; set; }

    public override string ToString()
    {
        return $"Title: {Title}\nHeader: {Header}\nContent: {Content}\nFooter: {Footer}\n";
    }
}

// Клас, който създава уеб страници
public class WebPageBuilder
{
    private WebPage webPage;

    public WebPageBuilder()
    {
        webPage = new WebPage();
    }

    public WebPageBuilder SetTitle(string title)
    {
        webPage.Title = title;
        return this;
    }

    public WebPageBuilder SetHeader(string header)
    {
        webPage.Header = header;
        return this;
    }

    public WebPageBuilder SetContent(string content)
    {
        webPage.Content = content;
        return this;
    }

    public WebPageBuilder SetFooter(string footer)
    {
        webPage.Footer = footer;
        return this;
    }

    public WebPage Build()
    {
        return webPage;
    }
}

// Клас, който създава уеб страници с определени статични стойности
public class WebPageDirector
{
    private WebPageBuilder builder;

    public WebPageDirector(WebPageBuilder builder)
    {
        this.builder = builder;
    }

    public void CreateArticle(string content)
    {
        builder.SetTitle("Article Title")
               .SetHeader("Article Header")
               .SetContent(content)
               .SetFooter("Article Footer");
    }

    public void CreateForm(string title, string fields)
    {
        builder.SetTitle(title)
               .SetHeader("Form Header")
               .SetContent($"Form Fields: {fields}")
               .SetFooter("Form Footer");
    }
}

class Program
{
    static void Main()
    {
        // Пример за използване на класовете
        WebPageBuilder builder = new WebPageBuilder();
        WebPageDirector director = new WebPageDirector(builder);

        // Създаване на уеб страница от тип "Article"
        director.CreateArticle("This is the content of the article.");
        WebPage articlePage = builder.Build();
        Console.WriteLine("Article Page:\n" + articlePage);

        // Създаване на уеб страница от тип "Form"
        director.CreateForm("Registration Form", "Name, Email, Password");
        WebPage formPage = builder.Build();
        Console.WriteLine("Form Page:\n" + formPage);

    }
}

