---
title: "連接到 Sybase (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ebf5f7f5c12a8a2e3af85ba2901e2348da92c30b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="connect-to-sybase-sybasetosql"></a>連接到 Sybase (SybaseToSQL)
使用**連接到 Sybase**對話方塊連接到您想要移轉的 Sybase Adaptive Server Enterprise (ASE) 執行個體。  
  
若要存取此對話方塊，請在**檔案**功能表上，選取**連接到 Sybase**。 如果您之前已連線，則命令是**重新連接到 Sybase**。  
  
## <a name="options"></a>選項。  
**提供者**  
選取任何連接到 Sybase 伺服器電腦上已安裝的提供者。  
  
**模式**  
選取其中一個標準或進階連線模式。 在標準模式中，您可以輸入或選取的伺服器名稱、 連接埠、 使用者名稱和密碼值。 在進階模式下，您必須提供連接字串。  
  
**伺服器名稱**  
輸入或選取的名稱或 IP 位址的自動調整的伺服器。 預設伺服器名稱是電腦名稱相同。 這是標準模式選項。  
  
**伺服器通訊埠**  
如果您使用非預設連接埠連接到 ASE，輸入連接埠號碼。 預設連接埠號碼為 5000。 這是標準模式選項。  
  
**User name**  
輸入用來連接到 ASE 的使用者名稱。 這是標準模式選項。  
  
**密碼**  
請輸入使用者名稱的密碼。 這是標準模式選項。  
  
**連接字串**  
輸入連接 ASE 完整連接字串。  
  
連接字串是由參數名稱 / 值組所組成。 參數的名稱會隨正在使用的提供者。  
  
**各種提供者的連接參數如下所示：**  
  
1.  連接參數**OLE DB 提供者**  
  
    |設定|Sybase 12.5 參數|Sybase 15 參數|  
    |-----------|-------------------------|-----------------------|  
    |伺服器名稱|伺服器名稱|[伺服器]|  
    |通訊埠|伺服器連接埠位址|通訊埠|  
    |[使用者名稱]|使用者識別碼|使用者識別碼|  
    |[密碼]|[密碼]|[密碼]|  
    |提供者|提供者|提供者|  
  
    Sybase ASE 12.5，連接字串範例如下：  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    適用於 Sybase ASE 15，連接字串範例如下所示：  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  連接參數**ODBC 提供者**  
  
    |設定|Sybase 12.5/15 參數|  
    |-----------|-----------------------------|  
    |驅動程式名稱|驅動程式|  
    |伺服器名稱|[伺服器]|  
    |使用者名稱|uid|  
    |[密碼]|Pwd|  
    |通訊埠編號|通訊埠|  
  
    Sybase ASE 12.5 或 15，連接字串範例如下所示：  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  連接參數**ADO.NET 提供者**  
  
    |設定|Sybase 12.5/15 參數|  
    |-----------|-----------------------------|  
    |伺服器名稱|[伺服器]|  
    |使用者名稱|uid|  
    |[密碼]|Pwd|  
    |通訊埠編號|通訊埠|  
  
    ADO.NET 提供者的連接字串的範例是如下：  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
如需詳細資訊，請參閱 ASE 文件。  
  
這是進階的模式選項。  
  
