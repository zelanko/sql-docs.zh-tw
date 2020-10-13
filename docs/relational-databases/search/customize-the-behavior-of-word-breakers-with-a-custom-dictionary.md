---
description: 使用自訂字典自訂文字分隔行為 (SQL Server 搜尋)
title: 使用自訂字典自訂文字分隔行為
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 46fb0f6fa4e8607296ead7a2f5e77ac97e75f9d5
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866982"
---
# <a name="customize-behavior-of-word-breakers-with-a-custom-dictionary-sql-server-search"></a>使用自訂字典自訂文字分隔行為 (SQL Server 搜尋)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  您可以建立語言特有自訂字典檔案，以自訂特定語言之斷詞工具的行為。 例如，您可以防止斷詞工具中斷特定詞彙或模式。  
  
 如需詳細資訊，請參閱下列 SharePoint 文章：  
  
 [建立自訂字典 (SharePoint Server 2010)](/previous-versions/office/sharepoint-server-2010/cc263242(v=office.14))  
  
 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，將自訂字典檔案放入下列資料夾中：  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 建立或變更自訂字典檔案之後，請使用下列命令重新啟動 SQL 全文檢索背景程式啟動器：  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
