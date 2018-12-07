---
title: SQL Server Data Tools | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.errortask.generichelp
ms.assetid: 5f08f15a-851d-4026-a557-28b3c6492efe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77d24c998c17e9fb265defa252b37b955e451bda
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52414665"
---
# <a name="sql-server-data-tools"></a>SQL Server Data Tools
SQL Server Data Tools (SSDT) 透過導入常見的宣告式模型轉換資料庫開發，此模型橫跨 Visual Studio 內的所有資料庫開發階段。 您可以使用 SSDT Transact\-SQL 設計功能建置、偵錯、維護和重構資料庫。 您可以使用資料庫專案，或直接使用位於內部或外部部署之連接的資料庫執行個體。  
  
開發人員可以使用熟悉 Visual Studio 工具來開發資料庫。 工具包含：Transact\-SQL 編輯器中的程式碼巡覽、IntelliSense、可供 C# 和 Visual Basic 平行設計的語言支援、平台特定的驗證、偵錯與宣告式編輯。 SSDT 還提供視覺化資料表設計工具，以用於在資料庫專案或連接的資料庫執行個體中建立及編輯資料表。 在以小組為主的環境下處理資料庫專案時，您可以使用所有檔案的版本控制。 到了發行專案的時候，您可以發行至所有支援的 SQL 平台，包括 SQL Database 和 SQL Server。 SSDT 平台驗證功能可確保指令碼能在指定的平台上運作。  
  
Visual Studio 中的 SQL Server 物件總管提供資料庫物件的檢視，類似於 SQL Server Management Studio。 SQL Server 物件總管可讓您執行輕型資料庫管理和設計工作。 您可以輕鬆地建立、編輯、重新命名及刪除資料表、預存程序、類型和函式。 您也可直接從 SQL Server 物件總管使用關聯式功能表編輯資料表資料、比較結構描述或執行查詢。  
  
以下主題和章節討論 SSDT 如何有助於資料庫開發工作。 加入 HOW TO 主題的目的是要協助引導您完成資料庫專案工作。 這些工作 (撰寫方式像教學課程而且依序完成) 使用 Northwind Traders，這是一家進出口特色食品的虛構公司。  
  
|主題/章節|Description|  
|-------------------|---------------|  
|[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)|本節的主題將說明用於撰寫、建置、偵錯及發行資料庫專案的 SQL Server Data Tools 功能。|  
|[使用命令列工具進行專案導向的資料庫開發](../ssdt/project-oriented-database-development-using-command-line-tools.md)|本節的主題將說明讓您應用於一些專案導向之資料庫開發狀況的命令列工具。|  
|[連接的資料庫開發](../ssdt/connected-database-development.md)|本節的主題將說明用於設計及查詢連接之資料庫的 SQL Server Data Tools 功能。|  
|[使用參考資料庫中的資料比較和同步處理一個或多個資料表中的資料](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)|討論如何比較來源資料庫和目標資料庫中的資料、指定應該比對的值，然後更新目標以同步處理資料庫，或將更新指令碼匯出到 Transact\-SQL 編輯器或檔案。|  
|[使用 Transact-SQL 編輯器，編輯及執行指令碼](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)|本節的主題將說明如何使用 Transact\-SQL 編輯器，它可在您使用指令碼時提供豐富的編輯和偵錯體驗。|  
|[管理資料表、關聯性及修正錯誤](../ssdt/manage-tables-relationships-and-fix-errors.md)|本節的主題將說明如何：<br /><br />-   使用資料表設計工具，設計資料表及管理資料表關聯性。<br />-   修正一般語法或語意錯誤。|  
|[使用 SQL Server 單元測試驗證資料庫程式碼](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)|討論如何使用 SQL Server 單元測試來建立資料庫的基準狀態，然後驗證您對資料庫物件所做的任何後續變更。|  
|[擴充資料庫功能](../ssdt/extending-the-database-features.md)|您可以建立擴充功能，讓您擴充單元測試和資料庫程式碼分析這類功能。|  
|[SQL Server Data Tools 的必要權限](../ssdt/required-permissions-for-sql-server-data-tools.md)|討論使用 SQL Server Data Tools 時的必要存取權限。|  
|[DAC Framework 相容性](../ssdt/dac-framework-compatibility.md)|描述 DAC 架構的相容性問題。|  
  

  
