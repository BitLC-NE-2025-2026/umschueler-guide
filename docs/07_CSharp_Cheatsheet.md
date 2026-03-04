# 💻 C# OOP & ASP.NET Core Cheatsheet

![C#](https://img.shields.io/badge/CSharp-OOP_&_UML-239120?style=for-the-badge&logo=csharp&logoColor=white) ![ASP.NET](https://img.shields.io/badge/ASP.NET_Core-MVC-512BD4?style=for-the-badge&logo=dotnet) ![MVC](https://img.shields.io/badge/Architektur-MVC_Pattern-orange?style=for-the-badge)

Hier ist eine schnelle und hochverdichtete Übersicht über die wichtigsten Konzepte in C# (objektorientierte Programmierung) und dem ASP.NET Core Framework. Perfekt als Last-Minute-Wiederholung für die IHK AP1 und AP2.

---

## 📑 Inhaltsverzeichnis
1. [🏛️ Objektorientierte Programmierung (OOP)](#-objektorientierte-programmierung-oop)
2. [🌐 ASP.NET Core (MVC Architektur)](#-aspnet-core-mvc-architektur)

---

## 🏛️ Objektorientierte Programmierung (OOP)

<details open>
<summary><b>Die 4 Säulen der OOP</b></summary>
1. **Kapselung (Encapsulation):** Verstecken des internen Zustands durch `private` Felder und die Offenlegung kontrollierter Zugriffe via `public` Properties (Getter/Setter).
2. **Abstraktion (Abstraction):** Verbergen komplexer Implementierungsdetails. Nur die nötigen Schnittstellen (`interface`, `abstract class`) sind nach außen sichtbar.
3. **Vererbung (Inheritance):** Eine abgeleitete Klasse erbt Felder, Properties und Methoden von einer Basisklasse (Vermeidet redundanten Code, "Ist-Ein"-Beziehung: *Ein Hund ist ein Tier*). In C# deklariert mit `:`.
4. **Polymorphie (Polymorphism):** Methoden können in abgeleiteten Klassen mit `override` überschrieben werden oder Interfaces können auf völlig unterschiedliche Weise implementiert werden.
</details>

<details open>
<summary><b>Interfaces vs. Abstract Classes</b></summary>
- **Interface:** Definiert nur den *Vertrag* (Methodensignaturen), **ohne** jegliche Logik. Eine Klasse kann **mehrere** Interfaces implementieren (Mehrfachvererbung-Ersatz).
- **Abstract Class:** Kann sowohl *abstrakte Methoden* (ohne Logik) als auch *echte Logik/Felder* enthalten. Man kann davon keine Instanz (`new()`) bilden. Klassen können in C# nur **von genau einer** abstrakten Basisklasse erben.
</details>

<details open>
<summary><b>SOLID Prinzipien (Die saubere Architektur)</b></summary>
- **S**ingle Responsibility Principle: Eine Klasse sollte nur einen einzigen Grund haben, sich zu ändern (nur für eine ganz spezifische Sache verantwortlich sein).
- **O**pen/Closed Principle: Klassen sollten *offen für Erweiterungen*, aber *geschlossen für Veränderungen* des bestehenden Codes sein.
- **L**iskov Substitution Principle: Objekte einer Basisklasse müssen jederzeit durch Objekte abgeleiteter Klassen ersetzt werden können, ohne das Programm zum Absturz zu bringen.
- **I**nterface Segregation Principle: Viele kleine, extrem spezifische Interfaces sind viel besser als ein riesiges "Gott-Interface", das Klassen zwingt Methoden zu implementieren, die sie gar nicht brauchen.
- **D**ependency Inversion Principle: Abhängigkeiten sollten zu Abstraktionen (Interfaces) bestehen, nicht zu konkreten Implementierungen. 
</details>

---

## 🌐 ASP.NET Core (MVC Architektur)

<details open>
<summary><b>Das MVC Pattern</b></summary>
- **M (Model):** Repräsentiert die Struktur der Daten und die Geschäftslogik. Wird in ASP.NET oft noch feiner unterteilt in *Entities* (für die Datenbank) und *ViewModels* (für die Benutzeroberfläche).
- **V (View):** Das, was der Endanwender im Browser sieht (HTML / CSS). ASP.NET benutzt die geniale **Razor**-Syntax (`.cshtml`), um C#-Code nahtlos mit HTML zu mischen (`@Model.Name`).
- **C (Controller):** Das Gehirn der Anwendung. Nimmt HTTP-Anfragen (GET, POST) entgegen, greift auf die Datenbank/Models zu und gibt am Ende die passende View (oder JSON) zurück.
</details>

<details open>
<summary><b>Dependency Injection (In der `Program.cs`)</b></summary>

Statt tief verschachtelt `new Service()` im Controller aufzurufen, überlassen wir dem IoC-Container ("Inversion of Control") von ASP.NET die absolute Kontrolle. Der Container baut uns die Objekte automatisch zusammen.
```csharp
// In der Program.cs (Dienst-Registrierung):

// 1. Transient: Bei JEDEM Auflösen des Interfaces wird ein komplett neues Objekt erstellt.
builder.Services.AddTransient<IEmailSender, SmtpEmailSender>(); 

// 2. Scoped: Pro HTTP-Request (Klick auf der Website) wird exakt EIN Objekt erstellt. (Der absolute Standard für Datenbank-Zugriffe!)
builder.Services.AddScoped<IArticleRepository, DbArticleRepo>(); 

// 3. Singleton: EIN EINZIGES Objekt für die gesamte Lebensdauer der App. (Vorsicht vor Thread-Safety-Problemen!)
builder.Services.AddSingleton<ICacheService, MemoryCache>(); 
```
</details>

<details open>
<summary><b>Entity Framework Core (Der ORM)</b></summary>

Der "Object-Relational-Mapper". Er verwandelt unsere C#-Klassen (Models) magisch in echte SQL-Tabellen, ohne dass wir SQL schreiben müssen.

- Definiert durch `DbSet<Auto> Autos { get; set; }` in der zentralen `DbContext`-Klasse.
- **Der Migrations-Workflow:** 
  1. Änderungen an C#-Klassen vornehmen (z.B. neue Property `Farbe` hinzufügen).
  2. Im Terminal/Package Manager: `dotnet ef migrations add AddFarbeToAuto`
  3. Im Terminal/Package Manager: `dotnet ef database update` (Pusht die Änderungen in die SQL-DB).
- **LINQ Abfragen:** Werden blitzschnell via Extension Methods direkt auf die DB abgesetzt:
  ```csharp
  var alteAutos = _db.Autos.Where(a => a.Baujahr < 1990).ToList();
  ```
</details>

> [!TIP]
> **Für die Mündliche Prüfung (AP2):** Wenn du in deinem Projekt ASP.NET Core mit dem Entity Framework und Dependency Injection genutzt hast, sei darauf gefasst, dass die Prüfer genau diese drei Dinge im Fachgespräch abfragen werden! Sei bereit, "Inversion of Control" und den Sinn von "Migrations" lückenlos zu erklären.

---
[Zurück zur Übersicht](../README.md)
