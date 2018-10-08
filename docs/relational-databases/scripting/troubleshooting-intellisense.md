---
title: 針對 IntelliSense 進行疑難排解 (SQL Server Management Studio) | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- unavailable options [IntelliSense]
- IntelliSense [SQL Server], troubleshooting
- IntelliSense [SQL Server], unavailable options
- troubleshooting [IntelliSense]
ms.assetid: 4b72ffc6-aea2-4e11-ab36-fa2de4d7bcc5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93f7794061e2836dc3778c6ceaca056cc03c6f8c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813086"
---
# <a name="troubleshooting-intellisense"></a>針對 IntelliSense 進行疑難排解
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  在某些情況下，IntelliSense 選項的運作可能會不符合您的預期。  
  
## <a name="conditions-that-affect-intellisense"></a>影響 IntelliSense 的條件  
 下列條件可能會影響 IntelliSense 的行為：  
  
-   游標上面有程式碼發生錯誤。  
  
     如果在插入點位置之上，有不完整的陳述式或其他編碼錯誤，IntelliSense 可能無法剖析程式碼元素，因此，將無法運作。 您可以將適當的程式碼註解化來重新啟用 IntelliSense。  
  
-   插入點位於程式碼註解內。  
  
     如果插入點在來源檔案內的註解中，便無法使用 IntelliSense 選項。  
  
-   插入點位於字串常值內。  
  
     如果插入點在括住字串常值的引號內，便無法使用 IntelliSense 選項，例如：  
  
     `WHERE FirstName LIKE 'Patri%|'`  
  
-   已關閉自動選項。  
  
     依預設，許多 IntelliSense 功能都會自動運作，但您可以停用任何功能。  
  
     即使已停用自動完成陳述式的功能，您也可以使用 IntelliSense 功能。 如需詳細資訊，請參閱[設定 IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-intellisense-sql-server-management-studio.md)。  
  
## <a name="database-engine-query-intellisense"></a>Database Engine 查詢 IntelliSense  
 下列問題適用於 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 查詢編輯器：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中的 IntelliSense 功能不支援所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法元素。 參數說明不支援某些物件中的參數，例如擴充預存程序。 如需詳細資訊，請參閱 [IntelliSense 所支援的 Transact-SQL 語法](../../relational-databases/scripting/transact-sql-syntax-supported-by-intellisense.md)。  
  
-   只有當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 或更新版本的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 執行個體時，才能使用 IntelliSense。 當查詢編輯器連接至舊版 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時，則無法使用 IntelliSense。  
  
-   當 SQLCMD 模式開啟時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中的 IntelliSense 卻關閉。  
  
-   IntelliSense 功能不包含您的編輯器視窗連接到資料庫後，由另一個連接所建立的資料庫物件。 如果 IntelliSense 功能中遺漏物件，例如完成清單，您可以選擇三個機制的其中一個，以重新整理編輯器視窗的快取物件：  
  
    -   選取 **[編輯]** 功能表，選取 **[IntelliSense]**，再選取 **[重新整理本機快取]**。  
  
    -   使用 CTRL+Shift+R 鍵盤快速鍵。  
  
    -   中斷您的編輯視器窗與 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的連接，然後再重新連接。  
  
-   完成清單不包含您沒有權限的資料庫物件。 IntelliSense 旗標會參考您沒有權限的物件。 例如，如果您開啟其他使用者撰寫的指令碼，對於該使用者擁有權限而您沒有權限之物件的任何參考，都會標示為不正確。  
  
-   如果您喪失與 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的連接，完成清單可能會停止運作。 請重新連接到該執行個體。  
  
  
