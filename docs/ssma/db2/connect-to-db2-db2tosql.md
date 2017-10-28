---
title: "連接至 DB2 (DB2ToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 733fae47c5c74eb120b7f8719dd53675eb5b7e36
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-db2-db2tosql"></a>連接至 DB2 (DB2ToSQL)
使用**連接到 DB2**對話方塊連接到您想要移轉的 DB2 資料庫。  
  
若要存取此對話方塊，請在**檔案**功能表上，選取**連接到 DB2**。 如果您之前已連線，則命令是**重新連接至 DB2**。  
  
## <a name="options"></a>選項  
**提供者**  
選取連接至 DB2 資料庫的資料存取提供者。 可用的提供者是 DB2 用戶端提供者和 OLE DB 提供者。 預設值是 DB2 用戶端提供者。  
  
**模式**  
選取標準、 TNSNAME 或連接字串的模式。  
  
-   在標準模式中，您可以輸入或選取的提供者、 伺服器名稱、 伺服器連接埠、 DB2 SID、 使用者名稱和密碼值。  
  
-   在 TNSNAME 模式中，您輸入 DB2 資料庫、 使用者名稱和密碼連接識別的項 （TNS 別名）。  
  
-   在連接字串模式中，您必須提供連接字串。  
  
    > [!IMPORTANT]  
    > 不建議您使用連接字串模式，因為文字可能會包含密碼，而且它會以純文字傳送。  
  
預設為標準模式。  
  
**伺服器名稱**  
輸入 DB2 伺服器名稱。 預設伺服器名稱是電腦名稱相同。 這是標準模式選項。  
  
**伺服器通訊埠**  
如果您用來連接至 DB2 1521 （預設值） 以外的通訊埠編號，請輸入連接埠號碼。 這是標準模式選項。  
  
**連線識別碼**  
輸入 DB2 連接識別碼。 這是資料庫的別名，因為本機 tnsnames.ora 檔案中定義。  
  
這是 TNSNAME 模式選項。  
  
**DB2 SID**  
輸入資料庫的 SID。 SID 都是區分 DB2 資料庫的電腦上的識別項。 資料庫的預設 SID 是資料庫名稱的前八個字元。  
  
這是標準模式選項。  
  
**使用者名稱**  
輸入 SSMA 將用來連接到 DB2 資料庫的使用者名稱。  
  
**密碼**  
請輸入使用者名稱的密碼。  
  
**連接字串**  
> [!IMPORTANT]  
> 不建議您使用連接字串模式，因為文字可能會包含密碼，而且它會以純文字傳送。  
  
如果您使用的連接字串模式時，輸入完整連接字串連接至 DB2。  
  
連接字串是由參數名稱 / 值組所組成。  
  
-   OLE DB 連接字串資訊，請參閱[Microsoft OLE DB Provider for DB2](http://go.microsoft.com/fwlink/?LinkId=85640)在 MSDN Library 的發行項。  
  
SSMA 的連接字串，請一定要包含的提供者參數。 此外，請確定當您連接至 DB2 時，包含連接埠參數。  
  

