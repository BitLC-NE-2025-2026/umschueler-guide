# C# OOP & ASP.NET Core Cheatsheet

![C#](https://img.shields.io/badge/CSharp-OOP_&_UML-239120?style=for-the-badge&logo=csharp&logoColor=white) ![ASP.NET](https://img.shields.io/badge/ASP.NET_Core-MVC-512BD4?style=for-the-badge&logo=dotnet)

Hier ist eine schnelle und kompakte Übersicht über die wichtigsten Konzepte in C# (objektorientierte Programmierung) und dem ASP.NET Core Framework. Perfekt als Wiederholung für die IHK AP1 und AP2.

---

## 🏛️ Objektorientierte Programmierung (OOP)

<details>
<summary><b>Die 4 Säulen der OOP</b></summary>
1. **Kapselung (Encapsulation):** Verstecken des internen Zustands durch `private` Felder und die Offenlegung via `public` Properties (Getter/Setter).
2. **Abstraktion (Abstraction):** Verbergen komplexer Implementierungsdetails. Nur die nötigen Schnittstellen (`interface`, `abstract class`) sind nach außen sichtbar.
3. **Vererbung (Inheritance):** Eine abgeleitete Klasse erbt Felder, Properties und Methoden von einer Basisklasse (Verkürzter Code, "Ist-Ein"-Beziehung: `Hund ist ein Tier`). In C# möglich mit `:`.
4. **Polymorphie (Polymorphism):** Methoden können in abgeleiteten Klassen mit `override` überschrieben werden oder Interfaces können auf unterschiedliche Weise implementiert werden.
</details>

<details>
<summary><b>Interfaces vs. Abstract Classes</b></summary>
- **Interface:** Definiert nur den *Vertrag* (Methodensignaturen), ohne Logik. Eine Klasse kann **mehrere** Interfaces implementieren.
- **Abstract Class:** Kann sowohl abstrakte Methoden (ohne Logik) als auch echte Logik enthalten. Man kann davon keine Instanz (`new()`) bilden. Klassen können nur **von einer** abstrakten Basisklasse erben.
</details>

<details>
<summary><b>SOLID Prinzipien</b></summary>
- **S**ingle Responsibility Principle: Eine Klasse sollte nur einen einzigen Grund haben, sich zu ändern (nur für eine Sache verantwortlich sein).
- **O**pen/Closed Principle: Klassen sollten offen für Erweiterungen, aber geschlossen für Veränderungen sein.
- **L**iskov Substitution Principle: Objekte einer Basisklasse müssen durch Objekte abgeleiteter Klassen ersetzt werden können, ohne die Logik zu brechen.
- **I**nterface Segregation Principle: Viele kleine, spezifische Interfaces sind besser als ein riesiges "Gott-Interface".
- **D**ependency Inversion Principle: Abhängigkeiten sollten zu Abstraktionen (Interfaces) bestehen, nicht zu konkreten Implementierungen. (Wird z.B. durch Dependency Injection in ASP.NET realisiert).
</details>

---

## 🌐 ASP.NET Core (MVC Architektur)

<details>
<summary><b>Das MVC Pattern</b></summary>
- **M (Model):** Repräsentiert die Struktur der Daten (z.B. Klassen). Wird oft noch in Entities (für die Datenbank) und ViewModels (für die UI) unterteilt.
- **V (View):** Das, was der User im Browser sieht (HTML / CSS). ASP.NET benutzt die **Razor**-Syntax (`.cshtml`), um C#-Code mit HTML zu mischen.
- **C (Controller):** Das Gehirn. Nimmt HTTP-Anfragen (GET, POST) entgegen, greift auf die Datenbank/Models zu und gibt die passende View zurück.
</details>

<details>
<summary><b>Dependency Injection (Program.cs)</b></summary>
Statt `new Service()` im Controller aufzurufen, überlassen wir dem IoC-Container von ASP.NET die Kontrolle (Inversion of Control).
```csharp
// In der Program.cs:
builder.Services.AddTransient<IEmailSender, SmtpEmailSender>(); // Bei jedem MUSS ein neues Objekt erstellt werden.
builder.Services.AddScoped<IArticleRepository, DbArticleRepo>(); // Pro HTTP-Request EIN Objekt. (Standard für DB)
builder.Services.AddSingleton<ICacheService, MemoryCache>(); // EIN Objekt für die gesamte Lebensdauer der App.
```
</details>

<details>
<summary><b>Entity Framework Core (ORM)</b></summary>
Der Object-Relational-Mapper. Verwandelt C#-Models in SQL-Tabellen.
- `DbSet<Auto> Autos { get; set; }` in der `DbContext` Klasse.
- **Migrationen:** 
  1. Änderungen an C# Klassen vornehmen.
  2. `dotnet ef migrations add NameDerAenderung`
  3. `dotnet ef database update`
- **Linq Abfragen:** Oft als Extension Methods verwendet: `_db.Autos.Where(a => a.Baujahr > 1990).ToList();`
</details>

---

[Zurück zur Übersicht](../README.md)
