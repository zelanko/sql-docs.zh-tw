---
title: 連接到 DB2 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ab734e93743d3a3158feb16dba044b58e7f48f23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299157"
---
# <a name="connect-to-db2-db2tosql"></a>連接到 DB2 (DB2ToSQL)
使用**連接到 DB2**對話方塊連接到您想要移轉的 DB2 資料庫。  
  
若要存取此對話方塊中，在**檔案**功能表上，選取**連接到 DB2**。 如果您先前曾經連線，則命令是**重新連接至 DB2**。  
  
## <a name="options"></a>選項  
**提供者**  
選取您的連線到 DB2 資料庫的資料存取提供者。 可用的提供者是 DB2 用戶端提供者和 OLE DB 提供者。 預設值是 DB2 用戶端提供者。  
  
**模式**  
選取 標準、 TNSNAME 或 連接字串的模式。  
  
-   在標準模式中，您可以輸入或選取的提供者、 伺服器名稱、 伺服器連接埠、 DB2 SID、 使用者名稱和密碼值。  
  
-   在 TNSNAME 模式中，您可以輸入 DB2 資料庫、 使用者名稱和密碼的連接的識別碼 （TNS 別名）。  
  
-   在連接字串模式中，您可以提供連接字串。  
  
    > [!IMPORTANT]  
    > 不建議您使用連接字串模式，因為文字可能會包含密碼，而且它以純文字傳送。  
  
預設為標準模式。  
  
**伺服器名稱**  
輸入 DB2 伺服器名稱。 預設伺服器名稱是電腦名稱相同。 這是標準模式的選項。  
  
**伺服器通訊埠**  
如果您用來連接至 DB2 1521 （預設值） 以外的連接埠號碼，請輸入連接埠號碼。 這是標準模式的選項。  
  
**連線識別碼**  
輸入 DB2 connect 識別項。 本機 tnsnames.ora 檔案中定義，這是資料庫的別名。  
  
這是 TNSNAME 模式選項。  
  
**DB2 SID**  
輸入資料庫的 SID。 SID 是區分電腦上的 DB2 資料庫的識別碼。 資料庫的預設值 SID 是資料庫名稱的前八個字元。  
  
這是標準模式的選項。  
  
**使用者名稱**  
輸入 SSMA 將用來連接到 DB2 資料庫的使用者名稱。  
  
**密碼**  
請輸入使用者名稱的密碼。  
  
**連接字串**  
> [!IMPORTANT]  
> 不建議您使用連接字串模式，因為文字可能會包含密碼，而且它以純文字傳送。  
  
如果您使用的連接字串模式，輸入完整的連接字串連接至 DB2。  
  
連接字串是由參數名稱和值配對所組成。  
  
-   OLE DB 連接字串資訊，請參閱[Microsoft OLE DB Provider for DB2](https://go.microsoft.com/fwlink/?LinkId=85640)在 MSDN Library 文章。  
  
SSMA 的連接字串，請一律包含提供者參數。 此外，請確定當您連接到 DB2 時，包含連接埠參數。  
  
