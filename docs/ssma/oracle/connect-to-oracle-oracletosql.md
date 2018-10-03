---
title: 連接到 Oracle (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 3e2e84fd2117afe15075084741e65989a30960cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674172"
---
# <a name="connect-to-oracle-oracletosql"></a>連線到 Oracle (OracleToSQL)
使用**連接到 Oracle**對話方塊連接到您想要移轉的 Oracle 資料庫。  
  
若要存取此對話方塊中，在**檔案**功能表上，選取**連接到 Oracle**。 如果您先前曾經連線，則命令是**重新連接到 Oracle**。  
  
## <a name="options"></a>選項。  
**提供者**  
選取您的連線到 Oracle 資料庫的資料存取提供者。 可用的提供者是 Oracle 用戶端提供者和 OLE DB 提供者。 預設值是 Oracle 用戶端提供者。  
  
**模式**  
選取 標準、 TNSNAME 或 連接字串的模式。  
  
-   在標準模式中，您可以輸入或選取的提供者、 伺服器名稱、 伺服器連接埠、 Oracle SID、 使用者名稱和密碼值。  
  
-   在 TNSNAME 模式中，您可以輸入 Oracle 資料庫、 使用者名稱和密碼的連接識別碼 （TNS 別名）。  
  
-   在連接字串模式中，您可以提供連接字串。  
  
    > [!IMPORTANT]  
    > 不建議您使用連接字串模式，因為文字可能會包含密碼，而且它以純文字傳送。  
  
預設為標準模式。  
  
**伺服器名稱**  
輸入 Oracle 伺服器名稱。 預設伺服器名稱是電腦名稱相同。 這是標準模式的選項。  
  
**伺服器通訊埠**  
如果您用來連接到 Oracle 1521 （預設值） 以外的連接埠號碼，請輸入連接埠號碼。 這是標準模式的選項。  
  
**連線識別碼**  
輸入 Oracle 連接識別碼。 本機 tnsnames.ora 檔案中定義，這是資料庫的別名。  
  
這是 TNSNAME 模式選項。  
  
**Oracle SID**  
輸入資料庫的 SID。 SID 是區分電腦上的 Oracle 資料庫的識別碼。 資料庫的預設值 SID 是資料庫名稱的前八個字元。  
  
這是標準模式的選項。  
  
**使用者名稱**  
輸入 SSMA 將用來連接到 Oracle 資料庫的使用者名稱。  
  
**密碼**  
請輸入使用者名稱的密碼。  
  
**連接字串**  
> [!IMPORTANT]  
> 不建議您使用連接字串模式，因為文字可能會包含密碼，而且它以純文字傳送。  
  
如果您使用的連接字串模式，輸入完整的連接字串連接到 Oracle。  
  
連接字串是由參數名稱和值配對所組成。  
  
-   OLE DB 連接字串資訊，請參閱[Microsoft OLE DB Provider for Oracle](http://go.microsoft.com/fwlink/?LinkId=85640)在 MSDN Library 文章。  
  
SSMA 的連接字串，請一律包含提供者參數。 此外，請確定您包含連接埠參數，當您連接到 Oracle。  
  
