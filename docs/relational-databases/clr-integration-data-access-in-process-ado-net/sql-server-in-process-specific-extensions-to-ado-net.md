---
title: Ado.net 的 SQL Server 同處理序特定擴充 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data access [CLR integration]
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], in-process extensions
- in-process data access providers [CLR integration]
- extensions [CLR integration]
ms.assetid: 781b812e-eb14-472a-85fa-aa4cdb929bee
author: rothja
ms.author: jroth
ms.openlocfilehash: b1ed0cf58c34506ce12dd04bf529a80d44a03d2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951682"
---
# <a name="sql-server-in-process-specific-extensions-to-adonet"></a>ADO.NET 的 SQL Server 同處理序特定擴充
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ADO.NET 有四個專門用於同處理序的主要功能擴充。 下列主題將詳細說明這些擴充功能。  
  
## <a name="in-this-section"></a>本節內容  
 [SqlContext 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlcontext-object.md)  
 此類別會摘要執行 Managed 程式碼同處理序之 SQL Server 常式呼叫者的內容，藉以存取其他延伸模組。  
  
 [SqlPipe 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)  
 此類別包含可將表格式結果和訊息傳送到用戶端的常式。  
  
 [SqlTriggerContext 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)  
 此類別提供執行觸發程序之內容的相關資訊。  
  
 [SqlDataRecord 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)  
 SqlDataRecord 類別會要求單一資料列的資料及其相關的中繼資料，並允許預存程序將自訂結果集傳回用戶端。  
  
  
