---
title: 連接到 Sybase （SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6cb2f4196737cceec2f60684de1b7409f5e383a0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083387"
---
# <a name="connect-to-sybase-sybasetosql"></a>連線到 Sybase (SybaseToSQL)
使用 [**連接到 sybase** ] 對話方塊，即可連接到您想要遷移的 Sybase 自我調整伺服器 ENTERPRISE （ASE）實例。  
  
若要存取此對話方塊，請在 [檔案]**功能表上，選取 [連線****到 Sybase]**。 如果您先前已連線，此命令會**重新連接到 Sybase**。  
  
## <a name="options"></a>選項。  
**提供者**  
選取電腦上任何已安裝的提供者，以連接到 Sybase 伺服器。  
  
**模式**  
選取 [標準] 或 [advanced] 連接模式。 在 [標準模式] 中，您可以輸入或選取伺服器名稱、埠、使用者名稱和密碼的值。 在 [advanced] 模式中，您會提供連接字串。  
  
**伺服器名稱**  
輸入或選取適應性伺服器的名稱或 IP 位址。 預設的伺服器名稱與電腦名稱稱相同。 這是標準模式選項。  
  
**伺服器埠**  
如果您使用非預設埠連接至 ASE，請輸入埠號碼。 預設埠號碼為5000。 這是標準模式選項。  
  
**使用者名稱**  
輸入用來連接 ASE 的使用者名稱。 這是標準模式選項。  
  
**密碼**  
輸入使用者名稱的密碼。 這是標準模式選項。  
  
**連接字串**  
輸入 ASE 連接的完整連接字串。  
  
連接字串是由參數名稱和值配對所組成。 參數的名稱會隨所使用的提供者而有所不同。  
  
**各種提供者的連接參數如下：**  
  
1.  **OLE DB 提供者**的連接參數  
  
    |設定|Sybase 12.5 參數|Sybase 15 參數|  
    |-----------|-------------------------|-----------------------|  
    |伺服器名稱|伺服器名稱|伺服器|  
    |連接埠|伺服器埠位址|連接埠|  
    |使用者名稱|使用者識別碼|使用者識別碼|  
    |密碼|密碼|密碼|  
    |提供者|提供者|提供者|  
  
    針對 Sybase ASE 12.5，範例連接字串如下所示：  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    對於 Sybase ASE 15，範例連接字串如下所示：  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  **ODBC 提供者**的連接參數  
  
    |設定|Sybase 12.5/15 參數|  
    |-----------|-----------------------------|  
    |驅動程式名稱|driver|  
    |伺服器名稱|伺服器|  
    |使用者名稱|Uid|  
    |密碼|Pwd|  
    |連接埠號碼|連接埠|  
  
    針對 Sybase ASE 12.5 或15，連接字串的範例如下所示：  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  **ADO.NET 提供者**的連接參數  
  
    |設定|Sybase 12.5/15 參數|  
    |-----------|-----------------------------|  
    |伺服器名稱|伺服器|  
    |使用者名稱|Uid|  
    |密碼|Pwd|  
    |連接埠號碼|連接埠|  
  
    ADO.NET 提供者連接字串的範例如下所示：  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
如需詳細資訊，請參閱 ASE 檔。  
  
這是先進的模式選項。  
  
