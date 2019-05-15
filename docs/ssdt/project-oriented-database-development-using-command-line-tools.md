---
title: 使用命令列工具進行專案導向的資料庫開發 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9a26def9-8fbd-43e4-9e57-414840b73ed8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7cf13ec0608dd3340e37307f5040172311ed7463
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65101855"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>使用命令列工具進行專案導向的資料庫開發
SQL Server Data Tools 提供命令列工具以讓您應用於一些專案導向的資料庫開發案例。  
  
## <a name="in-this-section"></a>本節內容  
  
|||  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage.md)|本主題將說明用於下列工作的 SQLPackage.exe 公用程式：<br /><br />-   從即時 SQL Server 資料庫擷取 .dacpac 檔案。<br />-   將 .dacpac 檔案發行至即時 SQL Server 資料庫，以便累加更新即時資料庫結構描述，使其符合該 .dacpac。<br />-   將 .dacpac 檔案與即時 SQL Server 資料庫進行比較，並產生累加式升級 Transact\-SQL 指令碼而無須更新即時資料庫。<br />-   比較兩個 .dacpac 檔案以產生累加式升級 Transact\-SQL 指令碼。<br />-   產生 XML 報表以列出一旦資料庫進行累加式升級後，累加式升級可能造成的變更摘要。|  
|[搭配 dbSqlPackage 提供者使用 MSDeploy](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|本主題將說明用於下列工作的 [Web Deployment Tool](https://go.microsoft.com/fwlink/?LinkId=231798) 提供者 (隨附於 SSDT 且名為 dbSqlPackage)，可搭配 Microsoft Internet Information Services (IIS) Web Deployment Tool (MSDeploy.exe) 運作：<br /><br />-   從遠端/本機 SQL Server 或 SQL Azure 資料庫擷取 .dacpac 檔案。<br />-   將 .dacpac 發行至遠端/本機 SQL Server 或 SQL Azure 資料庫，以累加升級資料庫。<br />-   從本機 SQL Server 資料庫發行至遠端 SQL Server 或 SQL Azure 資料庫，以累加升級遠端資料庫。<br />-   將 .dacpac 與遠端/本機 SQL Server 或 SQL Azure 資料庫進行比較，以產生累加升級 Transact\-SQL 指令碼而無須更新即時資料庫。<br />-   產生 XML 報表以列出一旦資料庫進行累加式升級後，累加式升級可能造成的變更摘要。|  
  
## <a name="related-sections"></a>相關章節  
[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)  
  
