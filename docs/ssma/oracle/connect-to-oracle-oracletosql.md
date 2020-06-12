---
title: 連接到 Oracle （OracleToSQL） |Microsoft Docs
description: 瞭解如何連接到 Oracle 資料庫，以使用 SSMA for Oracle 開始進行遷移。 使用 [連接到 Oracle] 對話方塊。
authors: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
ms.author: alexiva
ms.openlocfilehash: 1c69ace09cccd3d87017fef5bae86e3c03a60ad8
ms.sourcegitcommit: 38639b67a135ca1a50a8e38fa61a089efe90e3f1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2020
ms.locfileid: "84454521"
---
# <a name="connect-to-oracle-oracletosql"></a>連接到 Oracle （OracleToSQL）

使用 [**連接到 oracle** ] 對話方塊，即可連接到您想要遷移的 Oracle 資料庫。

若要存取此對話方塊，請在 **[檔案**] 功能表上，選取 [**連接到 Oracle]**。 如果您先前已連線，此命令會**重新連接到 Oracle**。

## <a name="options"></a>選項

**提供者**  
選取您連接到 Oracle 資料庫的資料存取提供者。 可用的提供者為 Oracle 用戶端提供者和 OLE DB 提供者。 預設值為 [Oracle 用戶端提供者]。

**Mode**  
選取 [標準]、[TNSNAME] 或 [連接字串] 模式。

- 在標準模式中，您可以輸入或選取提供者、伺服器名稱、伺服器埠、Oracle SID、使用者名稱和密碼的值。
- 在 TNSNAME 模式中，您可以輸入 Oracle 資料庫的 connect 識別碼（TNS alias）、使用者名稱和密碼。
- 在 [連接字串模式] 中，您會提供連接字串。

  > [!IMPORTANT]
  > 我們不建議您使用連接字串模式，因為文字可能包含密碼，並以純文字傳送。

預設值為 [標準] 模式。

**伺服器名稱**  
輸入 [Oracle 伺服器名稱]。 預設的伺服器名稱與電腦名稱稱相同。 這是標準模式選項。

**伺服器通訊埠**  
如果您使用1521以外的通訊埠編號（預設值）來連接到 Oracle，請輸入埠號碼。 這是標準模式選項。

**Connect 識別碼**  
輸入 Oracle connect 識別碼。 這是在本機 tnsnames.ora. tnsnames.ora 檔案中定義的資料庫別名。

這是 TNSNAME 模式選項。

**Oracle SID**  
輸入資料庫的 SID。 SID 是用來區別電腦上 Oracle 資料庫的識別碼。 資料庫的預設 SID 是資料庫名稱的前八個字元。

這是標準模式選項。

**使用者名稱**  
輸入 SSMA 將用來連接到 Oracle 資料庫的使用者名稱。

**密碼**  
請輸入使用者名稱的密碼。

**連接字串**  
> [!IMPORTANT]
> 我們不建議您使用連接字串模式，因為文字可能包含密碼，並以純文字傳送。

如果您使用連接字串模式，請輸入 Oracle 連接的完整連接字串。

連接字串是由參數名稱和值配對所組成。

- 如需 OLE DB 連接字串資訊，請參閱 MSDN Library 上的[Microsoft OLE DB Provider for Oracle](https://go.microsoft.com/fwlink/?LinkId=85640)文章。

若為 SSMA 連接字串，請一律包含 Provider 參數。 此外，當您連接到 Oracle 時，請務必包含 Port 參數。

## <a name="next-steps"></a>後續步驟

遷移程式的下一個步驟是[連接到 SQL Server](connect-to-sql-server-oracletosql.md)。
