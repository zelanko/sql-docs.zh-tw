---
title: "架構概觀 (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c4a4f66-ea3e-4a73-acf2-6c8aeafc94b0
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# 架構概觀 (SQL Server R Services)
本節提供的架構概觀 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，包括安全性、 SQL Server 資料庫引擎中加入支援 R 元件和執行 SQL Server 中的開放原始碼 R 指令碼的互通性的新元件。


## 目標


架構的 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 設計來支援開放原始碼 R 語言。 R 的目前使用者應該能夠連接埠 R 程式碼，來執行在 T-SQL 中相當小的修改。

不過，SQL Server R 服務也提供創新技術，提供更高的效能和更緊密地資料庫整合的 R 語言，以啟用更快速的資料輸送量和處理，並降低企業開發 R 解決方案的障礙。 這些新功能包括開放原始碼和 Microsoft 開發的專屬的元件。


與 SQL Server 整合的主要目標是改善的效能和延展性提供，同時安全地管理資料。 朝這個目標，SQL Server R 服務會提供多處理序的基礎結構支援整合式的 Windows 驗證和密碼為基礎的 SQL 登入。 

+ [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 提供 R、 以及 ScaleR 封裝和以平行方式執行 R 工作的能力的基底分佈。
+ SQL Server 中的新元件執行外部指令碼，提供安全、 高效能的架構。
+ 在 SQL Server 處理序，以提供安全性和更高的管理性之外，R 工作執行。
+ [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 管理的所有 R 程序的安全性。 

為了協助您充分運用現有的 R 程式碼，並充分利用這些增強功能，本章節的主題會描述詳細資料中的新架構。 瞭解如何處理資料處理和分析的 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], ，您可以做出適當的選擇，有關如何擷取資料、 如何最有效率的方式執行特性工程設計，以及如何取用結果。
 

## 本節內容
+ [R 的互通性](../../advanced-analytics/r-services/r-interoperability-in-sql-server-r-services.md)
+ [R 服務的 SQL Server 中的新元件](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)
+ [安全性概觀](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)

## 另請參閱
[R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)
