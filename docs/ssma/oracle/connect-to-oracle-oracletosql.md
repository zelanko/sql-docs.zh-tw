---
title: "連接到 Oracle (OracleToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 6350438d06f574096f78c44af85a298b5003423a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="connect-to-oracle-oracletosql"></a>連接到 Oracle (OracleToSQL)
使用**Connect to Oracle**對話方塊連接到您想要移轉的 Oracle 資料庫。  
  
若要存取此對話方塊，請在**檔案**功能表上，選取**Connect to Oracle**。 如果您之前已連線，則命令是**重新連接到 Oracle**。  
  
## <a name="options"></a>選項。  
**提供者**  
選取您連接到 Oracle 資料庫的資料存取提供者。 可用的提供者是 Oracle 用戶端提供者和 OLE DB 提供者。 預設為 Oracle 用戶端提供者。  
  
**模式**  
選取標準、 TNSNAME 或連接字串的模式。  
  
-   在標準模式中，您可以輸入或選取的提供者、 伺服器名稱、 伺服器連接埠、 Oracle SID、 使用者名稱和密碼值。  
  
-   在 TNSNAME 模式中，您輸入 Oracle 資料庫、 使用者名稱和密碼的連接識別碼 （TNS 別名）。  
  
-   在連接字串模式中，您必須提供連接字串。  
  
    > [!IMPORTANT]  
    > 不建議您使用連接字串模式，因為文字可能會包含密碼，而且它會以純文字傳送。  
  
預設為標準模式。  
  
**伺服器名稱**  
輸入 Oracle 伺服器名稱。 預設伺服器名稱是電腦名稱相同。 這是標準模式選項。  
  
**伺服器通訊埠**  
如果您用來連接到 Oracle 1521 （預設值） 以外的通訊埠編號，請輸入連接埠號碼。 這是標準模式選項。  
  
**連線識別碼**  
輸入 Oracle 連接識別碼。 這是資料庫的別名，因為本機 tnsnames.ora 檔案中定義。  
  
這是 TNSNAME 模式選項。  
  
**Oracle SID**  
輸入資料庫的 SID。 SID 都是可辨別電腦上的 Oracle 資料庫的識別碼。 資料庫的預設 SID 是資料庫名稱的前八個字元。  
  
這是標準模式選項。  
  
**使用者名稱**  
輸入 SSMA 將用來連接到 Oracle 資料庫的使用者名稱。  
  
**密碼**  
請輸入使用者名稱的密碼。  
  
**連接字串**  
> [!IMPORTANT]  
> 不建議您使用連接字串模式，因為文字可能會包含密碼，而且它會以純文字傳送。  
  
如果您使用的連接字串模式時，輸入完整連接字串連接到 Oracle。  
  
連接字串是由參數名稱 / 值組所組成。  
  
-   OLE DB 連接字串資訊，請參閱[Microsoft OLE DB Provider for Oracle](http://go.microsoft.com/fwlink/?LinkId=85640)在 MSDN Library 的發行項。  
  
SSMA 的連接字串，請一定要包含的提供者參數。 此外，請確定您包含連接埠參數，當您連接到 Oracle。  
  
