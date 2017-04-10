---
title: "PolyBase 建立版本的功能摘要 | Microsoft Docs"
ms.custom: ""
ms.date: "04/13/2016"
ms.prod: "sql-non-specified"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
caps.latest.revision: 10
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 8
---
# PolyBase 建立版本的功能摘要
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  適用於 SQL Server 產品和服務的 PolyBase 功能摘要。  
  
## 產品版本的功能摘要  
 本表會摘要說明 PolyBase 的重要功能以及提供這些功能的產品。  
  
### [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
 這些功能適用於在內部部署或 Azure 虛擬機器中執行的 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  SQL Server 2014 和舊版不提供 PolyBase。  
  
|||  
|-|-|  
|**功能**|**可用性**|  
|使用下列項目查詢 Hadoop 資料： [!INCLUDE[tsql](../../includes/tsql-md.md)]|是|  
|使用下列項目查詢 Azure Blob 儲存體： [!INCLUDE[tsql](../../includes/tsql-md.md)]|是|  
|從 Hadoop 匯入資料|是|  
|從 Azure Blob 儲存體匯入資料|是|  
|匯出資料至 Hadoop|是|  
|匯出資料至 Azure Blob 儲存體|是|  
|從 Microsoft 的 BI 工具執行 PolyBase 查詢|是|  
|將查詢計算下推到 Hadoop|是|  
  
### [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
 這些功能適用於 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
|||  
|-|-|  
|**功能**|**可用性**|  
|使用下列項目查詢 Hadoop 資料： [!INCLUDE[tsql](../../includes/tsql-md.md)]|否|  
|使用下列項目查詢 Azure Blob 儲存體： [!INCLUDE[tsql](../../includes/tsql-md.md)]|是|  
|從 Hadoop 匯入資料|否|  
|從 Azure Blob 儲存體匯入資料|是|  
|匯出資料至 Hadoop|否|  
|匯出資料至 Azure Blob 儲存體|是|  
|從 Microsoft 的 BI 工具執行 PolyBase 查詢|是|  
|將查詢計算下推到 Hadoop|否|  
  
### [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 這些功能適用於 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
|||  
|-|-|  
|**功能**|**可用性**|  
|使用下列項目查詢 Hadoop 資料： [!INCLUDE[tsql](../../includes/tsql-md.md)]|是|  
|使用下列項目查詢 Azure Blob 儲存體： [!INCLUDE[tsql](../../includes/tsql-md.md)]|是|  
|從 Hadoop 匯入資料|是|  
|從 Azure Blob 儲存體匯入資料|是|  
|匯出資料至 Hadoop|是|  
|匯出資料至 Azure Blob 儲存體|是|  
|從 Microsoft 的 BI 工具執行 PolyBase 查詢|是|  
|將查詢計算下推到 Hadoop|是|  
  
## 另請參閱  
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)  
  
  