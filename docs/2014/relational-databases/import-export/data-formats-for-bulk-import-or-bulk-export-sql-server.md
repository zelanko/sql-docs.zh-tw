---
title: 大量匯入或大量匯出的資料格式 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c43cb42cffba31f20b0e9717204f5475b5bb156d
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012079"
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>大量匯入或大量匯出的資料格式 (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以接受字元資料格式或原生二進位資料格式的資料。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和其他應用程式 (例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) 之間，或其他資料庫伺服器 (例如 Oracle 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 之間移動資料時，請使用字元格式。 只有當您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之間傳送資料時，才能使用原生格式。  
  
 **本主題內容：**  
  
-   [大量匯入或匯出的資料格式](#ComponentsAndConcepts)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> 大量匯入或匯出的資料格式  
 下表根據資料的呈現方式和作業的來源或目標，指出一般適合使用的資料格式。  
  
|運算|原生|Unicode 原生|字元|Unicode 字元|  
|---------------|------------|--------------------|---------------|-----------------------|  
|使用不含任何擴充或雙位元組字集 (DBCS) 字元的資料檔，在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間進行大量傳送資料。 除非已使用格式檔案，否則必須以相同的方式定義這些資料表。|是<sup>1</sup>|-|-|-|  
|若為 `sql_variant` 資料行，使用原生資料格式是最佳方法，因為原生資料格式會保留每個 `sql_variant` 值的中繼資料，但字元或 Unicode 格式則不會。|是|-|-|-|  
|使用含有擴充或 DBCS 字元的資料檔，在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間進行大量傳送資料。|-|是|-|-|  
|從其他程式所產生的文字檔，大量匯入資料。|-|-|是|-|  
|將資料大量匯出至文字檔，以便使用於另一個程式之中。|-|-|是|-|  
|使用含有 Unicode 資料但不含擴充或 DBCS 字元的資料檔，在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之間進行大量傳送資料。|-|-|-|是|  
  
 <sup>1</sup>大量匯出資料最快的方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用時**bcp**。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [從舊版 SQL Server 匯入原生與字元格式資料](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [使用 bcp 指定相容性的資料格式 &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  
