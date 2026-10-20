# QA Automation Framework

![Java](https://img.shields.io/badge/Java-11%2B-orange)
![Selenium](https://img.shields.io/badge/Selenium-4.26-43B02A)
![TestNG](https://img.shields.io/badge/TestNG-7.9-red)
![Maven](https://img.shields.io/badge/Build-Maven-C71A36)

An end-to-end UI test automation framework built with **Selenium WebDriver, Java and TestNG**, using the **Page Object Model (POM)** design pattern. It automates the core shopping flow (login, add to cart, checkout) on [SauceDemo](https://www.saucedemo.com), a demo e-commerce site built for practising test automation.

## Features

- **Page Object Model:** each page (Login, Products, Cart, Checkout) is its own class, so tests stay readable and locator changes happen in one place.
- **Shared `Base` class:** handles browser setup, window maximizing, implicit waits and config loading.
- **Config-driven:** the browser and other settings come from `config.properties`.
- **Automatic driver management:** WebDriverManager downloads the right ChromeDriver, so there is nothing to install manually.
- **TestNG test lifecycle:** `@BeforeMethod` and `@AfterMethod` handle setup and teardown, and `testng.xml` defines the suite.
- **HTML reporting:** ExtentReports generates a report after every run.
- **Screenshot utility:** captures the browser state for failure analysis.

## Tech Stack

| Area | Tools |
|---|---|
| Language | Java |
| Automation | Selenium WebDriver 4.26 |
| Test runner | TestNG 7.9 |
| Build tool | Maven |
| Driver management | WebDriverManager 5.8 |
| Reporting | ExtentReports 5.1 |
| Logging | SLF4J + Logback |

## Project Structure

```
QA-Automation
├── pom.xml
├── testng.xml                      # Test suite definition
└── src
    ├── main/java/com/test
    │   ├── Base/Base.java          # Driver setup + config loading
    │   ├── Login/Login.java        # Login page object
    │   ├── Products/Products.java  # Products page object
    │   ├── Cart/Cart.java          # Cart page object
    │   ├── Checkout/Checkout.java  # Checkout page object
    │   └── ReportUtils
    │       ├── ExtentReport.java   # HTML report generator
    │       └── ScreenShots.java    # Screenshot helper
    └── test
        ├── java/com/test/LoginTest/LoginTest.java   # Test cases
        └── resources/config.properties              # Browser config
```

## Test Scenarios

| Test | What it verifies |
|---|---|
| `ValidLogin` | Logging in with valid credentials lands on the Swag Labs inventory page. |
| `EndCheckout` | A user can log in, add an item to the cart, fill in checkout details, finish the order and see the confirmation message. |

## Getting Started

### Prerequisites

- JDK 11 or higher
- Maven 3.6+
- Google Chrome (latest)

### Setup

```bash
git clone https://github.com/SKK402/QA-Automation.git
cd QA-Automation
mvn clean install -DskipTests
```

### Configuration

Edit `src/test/resources/config.properties`:

```properties
browser=chrome
```

## Running the Tests

Run all tests:

```bash
mvn test
```

Run a specific suite file:

```bash
mvn test -Dsurefire.suiteXmlFiles=testng.xml
```

Run a single test class:

```bash
mvn test -Dtest=LoginTest
```

## Reports

After a run, open the generated reports in the `test-output/` folder:

- `ExtentReport.html`: detailed ExtentReports dashboard
- `index.html` and `emailable-report.html`: standard TestNG reports

Screenshots are saved to the `screenshots/` folder.
