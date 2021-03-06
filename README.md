# Objective
This repository contains several report engines, mainly for explorer and try as a playground to test those report engines.

How is the functionality, what is reuqired on install and setup to work with .Net Core.

## Background
A new project is launch, to develop a ERP(Enterprise Resource Planning)/CMS (Content Management System) like system.

The front end will be Angular web application, the back end system will be separated as a standalone part to provide web service (web API)

We decided to build the back end by .Net Core with the "Entity Framework", "Code First Approach"

Therefore I need to exploe and test how the back end system satisfy the report generation functionality.

# Scope
Try and error for study how to implmenet report(xlsx, pdf) generation in C# .net Core5

## Back end engine/tools
- Crystal Report (excel, pdf) (Implemented)
- Jasper Report (excel, pdf) (Implemented)
- EPPlus (excel) (Implemented)
- iText (pdf) (Implemented)
- OpenXmlSDK (excel) (Testing)

## Front end engine/tools
below are easy to use in pure javascript, officially support NodeJs or having NodeJs version but node is it not necessary in read/write

the examples were not included in this project, becuase this project not focus on read/write in front end 

- parallax/jsPDF (write pdf)
- mozilla/pdf.js (read pdf)
- SheetJS (read/write excel)

# Demo
***Before you run (F5) on Visual Studio, make sure you read the preparation and completed the configuration***

If want to test the Crystal Report, change the startup project to "CoreSystemConsoleInNet"

- Crystal Report
> According to this article: https://answers.sap.com/questions/13029137/crystal-reports-for-visual-studio-and-net-core-5-a.html
> 
> Because of some low level reasons, Crystal Report must rely on .Net Framework, not planning to move go to support .Net core in future and now
> 
> If you must use Crystal Report for your .Net Core application
> 
> The offical solution was make your Crystal Report in a .net framework solution as a proxy server (API service)
> 
> for the walkthrough: https://medium.com/scrum-and-coke/view-crystal-report-in-pdf-with-angular-and-asp-net-rest-api-1d6c72168e7c
> solution example: https://github.com/workcontrolgit/CrystalReportWebAPI

If want to test others report program, change the startup project to "CoreSystemConsole"

- For Jasper Report
- EPPlus5
- iText7

After updated the startup project

Then, run (press F5) and wait its finish, the report should be generated and placed at the directory `tempRenderFolder`

# Conclusion
In general speaking, declear you need, excel or pdf or both, read or write or both

the generation approach listed below:

For excel

- front end, use javascript to generate xlsx (in xml format), less implement time, hard to do comprehensive layout
- back end, framework/engine providing a design tool to design and save the layout as a template, allowed to feed the data set(s) to template, to 
- back end, having a template excel in back end, read and copy the template then fill your data in the cell by row/column

For pdf

- front end/back end, use javascript to call pdf api, create pdf components with coordinate (width, height, x, y), hard to handle comprehensive layout
- front end, use canvas HTML element to capture the a specific area of screen in browser and print as a pdf
- front end, use javascript to call browser print function to print your page as a pdf
- back end, convert a excel to pdf
- back end, convert html (maybe with limited css) to pdf

## For excel manipulation read/write (xlsx, xls)
After the test, I rank the tool from 1 to bigger number, 1 is the most perferable.
1. EPPlus5, api is straight forward, easy to understand and use, implemented excel like behaviors, most advcanced features (chart, pivot table, header, footer, print number, cell validation..etc), support xlsx
2. Jasper Report, Java based program, officia provide a c# wrapped for call support xlsx, xls
3. OpenXmlSDK, microsoft provides basic API, required to read dehumanized, complex, extremely long documentation
4. Crystal Report, support xlsx, xls, bad excel generation because of the design, for details please read below 4 Urls
> https://archive.sap.com/documents/docs/DOC-39608
> 
> https://userapps.support.sap.com/sap/support/knowledge/en/1198296?fbclid=IwAR0_KR9veTxUJG_LituJlLSBYrvG6BZN3_OUm-JEZSiFa9enoZp-Jysa54Q
> 
> https://answers.sap.com/questions/424754/how-to-merge-columns-when-exporting-crystal-report.html?fbclid=IwAR0WjV8zsw_6Fd5OG3s-BNCyzbVuYToHD1xCMIgh0O1mNRFIqbEXSCrlcUA
> 
> https://stackoverflow.com/questions/28045209/can-grow-proprity-of-a-crystal-report-field-doesnt-push-down-lines-correctly?fbclid=IwAR2KEHM-rtmA-FHfun3NrsS_rDZLdVotuiy-14u_u7ih7vbgcjLsUoGQejA

## For pdf manipulation write
After the test, I rank the tool from 1 to bigger number, 1 is the most perferable.
1. puppeteer/puppeteer, PejmanNik/puppeteer-report
2. Crystal Report
3. iText7
4. Jasper Report


# Preparation
Before run the solution, please install the report engines and complete the configuration setup

The installation steps details are described below

for example, if you want to test the JasperReport, please install JasperReport and complete the config before you run (F5) the program

## Configuration

1. Control which reports you would like to test, comment and uncomment the lines in

> `SolutionRoot\CoreSystemConsole\Program.cs`

```
// Tick-off the Report Entity Program
//InvoiceProgram invoiceProgram = new InvoiceProgram();

//HitRateHTMLProgram hitRateHTMLProgram = new HitRateHTMLProgram();

//HitRateXMLProgram hitRateXMLProgram = new HitRateXMLProgram();

//EPPlus5XlsxTemplateProgram ePPlus5XlsxTemplateProgram = new EPPlus5XlsxTemplateProgram();

ITextGroupIPdfTemplateProgram iTextGroupIText5PdfTemplateProgram = new ITextGroupIPdfTemplateProgram();
```

2. Control the report generate folder, open and edit

> `SolutionRoot\CoreReport\VisualizationEntity.cs`

```
protected string tempRenderFolder = @"D:\\Temp"; // report will be generated in this directory
```

## Crystal Report
### Pre-installation
Before run, please install Crystal Reports, Developer for Visual Studio Downloads
https://wiki.scn.sap.com/wiki/display/BOBJ/Crystal+Reports%2C+Developer+for+Visual+Studio+Downloads

### Documentation
Connecting to Object Collections
https://help.sap.com/viewer/0d6684e153174710b8b2eb114bb7f843/SP21/en-US/45afd8f46e041014910aba7db0e91070.html

### Example and Tutorial
Tutorial: Connecting to Object Collections
https://help.sap.com/viewer/0d6684e153174710b8b2eb114bb7f843/SP21/en-US/45c50fec6e041014910aba7db0e91070.html

## Jasper Reports
### Pre-installation
Before run, please install .NET jsreport sdk(jsreport binary, jsreport local) by nuget
https://jsreport.net/learn/dotnet

### Documentation
jsreport documentation
https://jsreport.net/learn

Recipes
https://jsreport.net/learn/recipes

Templating engines
https://jsreport.net/learn/templating-engines

.Net local reporting
https://jsreport.net/learn/dotnet-local

.Net Client
https://jsreport.net/learn/dotnet-client

### Example and Tutorial
GitHub jsreport/jsreport-dotnet
https://github.com/jsreport/jsreport-dotnet

#### Page header, footer, page number
Merge dynamic header with items
 
https://playground.jsreport.net/w/admin/ihh7laK2

Merge header and footer with page numbers

https://playground.jsreport.net/w/admin/kMI4FBmw

Merge with render for every page enabled

https://playground.jsreport.net/w/admin/1A7l_UG_

## EPPlus5
EPPlus5 is open source, but you are required to purchase license for commercial use

The library(ies) were installed under the project through Package Manager Console

[EPPlus]:https://www.nuget.org/packages/EPPlus

```
Install-Package EPPlus -Version 5.8.0
```

## iText Group
Some products of iText 7 Suite is open source, but you are required to purchase license for commercial use

The library(ies) were installed under the project through Package Manager Console

[itext7]:https://github.com/itext/itext7-dotnet
[itext7.pdfhtml]:https://github.com/itext/i7n-pdfhtml

```
Install-Package itext7 -Version 7.1.16
Install-Package itext7.pdfhtml -Version 3.0.5
```


## Program Structure
I use "Design Pattern - Decorator" to separate the coding files by reporting enginer.
>Let's said a system contains many functions, a report function represented by a menu item in navigation menu.
>
>In general, a report function provides the selection criteria, user select the criteria 
>
>Then, click "Export Xlsx" or "Export Pdf" button to generate report file in xlsx, pdf as they want.

"Decorator" Design Pattern gives a report program easy to switch the report enginer, also allows different reports use various engines in a single system

https://www.dofactory.com/net/decorator-design-pattern#realworld
