---
title: "使用自訂字典自訂斷詞工具行為 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: af2354ef37936e5538d1b32243978a165f2c853e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>使用自訂字典自訂斷詞工具行為
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] 您可以建立特定語言的自訂字典檔案，以自訂特定語言之斷詞工具的行為。 例如，您可以防止斷詞工具中斷特定詞彙或模式。  
  
 如需詳細資訊，請參閱下列 SharePoint 文章：  
  
 [建立自訂字典 (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=215011)  
  
 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，將自訂字典檔案放入下列資料夾中：  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 建立或變更自訂字典檔案之後，請使用下列命令重新啟動 SQL 全文檢索背景程式啟動器：  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
