---
layout: post
title: Insider Trades Tracker
permalink: insider-trades-tracker
author: Punit Arani
date: Aug 15, 2022
summary: Tracks SEC Forms 4 to Parse and Analyze Trades in Realtime.
category: Quant
---

[GitHub](https://github.com/punitarani/InsiderTradesTracker)

- **Objective**: Develop a real-time monitoring and analysis system for insider trading activities by tracking SEC Form 4 filings, enabling investors and interested parties to gain valuable insights into corporate executives' transactions involving their company's stock.
- **Takeaway**: Hands-on experience in web scraping, data parsing, dashboard development, and building practical finance applications.
- **Status**: Complete

## Description

The Insider Trades Tracker automates the process of scraping, parsing, and analyzing SEC Form 4 filings, which report trades by corporate insiders. This application monitors the SEC's website to fetch new filings as they are posted. It uses libraries such as `beautifulsoup4` and `lxml` to extract key details like the insider's name, the type of transaction, the date, and the number of shares involved.

The data is processed and stored in formats supported by `pandas` and `pyarrow`, making the information easy to handle and analyze. For long-term storage and easy access, the data is also kept in a document database.

## Features

- **Real-time Monitoring**: Regularly updates by pulling the latest Form 4 filings from the SEC website.
- **Automated Parsing**: Automatically extracts necessary data from filings using `beautifulsoup4` and `lxml`, removing the need for manual input.
- **Data Storage**: Uses `pandas` and `pyarrow` to structure the data for easy manipulation and analysis, with a document database for storage.
- **User-friendly Dashboard**: Features a dashboard created with `dash` and `dash-bootstrap-components` that allows users to interactively explore and analyze the data.
- **Deployment and Testing**: Employs `gunicorn` for application deployment, `pyyaml` for configuration, and tools like `pytest`, `pylint`, and `coverage` to ensure the application is robust and maintainable.

## Significance

The Insider Trades Tracker provides essential insights into insider trading, streamlining the tracking and analysis of such activities. This automation reduces the workload typically associated with manual tracking and enhances the accuracy and speed of data analysis. The real-time update feature ensures that the information is always current, supporting timely and informed decision-making.

The application's design focuses on practicality and efficiency, adhering to software engineering best practices for reliability and scalability. It is a useful tool for anyone looking to understand insider trading dynamics more deeply.
