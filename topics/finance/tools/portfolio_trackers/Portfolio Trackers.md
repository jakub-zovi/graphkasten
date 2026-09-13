---
tags:
  - fin
  - fin/tools
created: 2025-05-04T08:08
modified: 2026-09-05T12:38
published:
sources:
  - "[12 Best Portfolio Analysis Tools](https://medium.com/@Max_Dividends/12-best-portfolio-analysis-tools-in-2024-f050785a3fcf)"
topics:
  - Portfolio Tracking
  - Portfolio Analysis
  - Personal Finance
authors:
  - Jakub
ai-assisted: false
hidden: false
public: true
---
# Portfolio Trackers
ChatGPT(4o)[^1]
> **Portfolio tracking tools** are applications or software platforms that help investors monitor and manage their investment portfolios.
## Current State
I need to setup infrastructure for tracking my portfolio and wealth in order make better financial decisions. Right now I only have a foggy mental model of my finances that definitely does not correctly reflect the reality. I do not have clear view of all of my monthly expense (eg. subscriptions).
## Selected Setup
The most optimal path looks like having Python scripts and using Google sheets. Plus the Python scripts can produce CSV that I can import into [[TradingView Portfolios]] and also works with it in the downstream tasks.
## List of Apps
### Solely Portfolio Trackers
- Open-source
	- [[Portfolio Performance]]
		- [Website Download](https://www.portfolio-performance.info/en/)
		- https://github.com/portfolio-performance/portfolio
			- **3.4k** stars
		- **Best option for investment portfolio tracking**
		- I am currently using this
		- Youtube Video - [Portfolio Performance Tutorial](https://www.youtube.com/watch?v=df0Rb3k0VSA)
	- [[wealthfolio]]
		- https://github.com/afadil/wealthfolio
			- **5.1k** stars
		- Desktop Investment Tracking Application
- Google Sheet Spreadsheet Templates
	- [Stock Portfolio Tracking Spreadsheet](https://docs.google.com/spreadsheets/d/1Ajox_mGj_prTqfIWSSF1xcaDEBm6ZuZZDInZ1Es-_bM/edit?gid=4#gid=4)
		- [My copy of it](https://docs.google.com/spreadsheets/d/1qaEEy8dEwWXVX9iFDGKLXlW0-Kbo8843OtmYvzbVPvI/edit?gid=4#gid=4)
	- [Investment Portfolio Tracker — a Spreadsheet for DIY Investors](https://themeasureofaplan.com/investment-portfolio-tracker/)
		- [My copy of it](https://docs.google.com/spreadsheets/d/13c3PwTJSirXunyee0WerGj4jPLYMGOeY3DuUKd5M4iw/edit?gid=2047973151#gid=2047973151)
- Proprietary (with free tier)
	- Google Finance
	- Yahoo Finance
	- [[Snowball Analytics]]
		- https://snowball-analytics.com/
		- Shown in https://www.youtube.com/watch?v=7O7MzihMdzw
	- [[getquin]] [getquin](https://www.getquin.com/portfolio-tracker/)
		- Tracker used by European Youtuber [Angelo Colombo](https://www.youtube.com/@AngeloColomboFi)
		- Supports IBKR, Trade 
	- [[TradingView Portfolios]] 
		- **This looks very good - simple and very straight forward**
		- https://www.tradingview.com/portfolios/
	- [Portseido](https://www.portseido.com/pricing/)
	- [[Simple Portfolio]]
		- https://simpleportfolio.app/pricing
		- Free preprocessing of broker exports
	- [sharesight](https://www.sharesight.com/)
	

[^1]: Prompt: "Can you explain what are portfolio tracking tools and list some that you know?"