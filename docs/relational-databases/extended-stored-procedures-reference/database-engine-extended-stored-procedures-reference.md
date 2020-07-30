---
title: 擴充預存程序程式設計人員參考 | Microsoft Docs
description: 瞭解資料庫引擎擴充預存程式如何提供以伺服器為基礎的應用程式開發介面（API），以擴充 SQL Server 功能。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], listed
ms.assetid: 4e9d0374-0927-4f17-bab9-2215b1b8fea8
author: rothja
ms.author: jroth
ms.openlocfilehash: a2830f920078a4e625e9ccf0fc13f376b3fd4107
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244008"
---
# <a name="database-engine-extended-stored-procedures---reference"></a>資料庫引擎擴充預存程序 - 參考
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)]擴充預存程式 API （先前為 Open 資料服務的一部分）會提供以伺服器為基礎的應用程式開發介面（API），以擴充 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 API 包含用來建置應用程式的 C 和 C++ 函數和巨集。  
  
 隨著 CLR 整合之類的更新和更強大技術的出現，擴充預存程序的需求也大致被取代。  
  
> [!IMPORTANT]  
>  您應該徹底檢閱擴充預存程序的原始程式碼，您也應該先測試編譯過的 DLL，才能將它們安裝在實際執行伺服器上。 如需安全性檢閱和測試的資訊，請參閱此 [Microsoft 網站](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)。  
  
## <a name="in-this-section"></a>本節內容  
  
:::row:::
    :::column:::
        [Data types (資料類型)](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_pfield](../../relational-databases/extended-stored-procedures-reference/srv-pfield-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_alloc](../../relational-databases/extended-stored-procedures-reference/srv-alloc-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_convert](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_pfieldex](../../relational-databases/extended-stored-procedures-reference/srv-pfieldex-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_describe](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_rpcdb](../../relational-databases/extended-stored-procedures-reference/srv-rpcdb-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_getbindtoken](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_rpcname](../../relational-databases/extended-stored-procedures-reference/srv-rpcname-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_got_attention](../../relational-databases/extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_rpcnumber](../../relational-databases/extended-stored-procedures-reference/srv-rpcnumber-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
        [srv_rpcoptions](../../relational-databases/extended-stored-procedures-reference/srv-rpcoptions-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_message_handler](../../relational-databases/extended-stored-procedures-reference/srv-message-handler-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_rpcowner](../../relational-databases/extended-stored-procedures-reference/srv-rpcowner-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_paramdata](../../relational-databases/extended-stored-procedures-reference/srv-paramdata-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_rpcparams](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_paraminfo](../../relational-databases/extended-stored-procedures-reference/srv-paraminfo-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_senddone](../../relational-databases/extended-stored-procedures-reference/srv-senddone-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_paramlen](../../relational-databases/extended-stored-procedures-reference/srv-paramlen-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_sendmsg](../../relational-databases/extended-stored-procedures-reference/srv-sendmsg-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_parammaxlen](../../relational-databases/extended-stored-procedures-reference/srv-parammaxlen-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_sendrow](../../relational-databases/extended-stored-procedures-reference/srv-sendrow-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_paramname](../../relational-databases/extended-stored-procedures-reference/srv-paramname-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_setcoldata](../../relational-databases/extended-stored-procedures-reference/srv-setcoldata-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_paramnumber](../../relational-databases/extended-stored-procedures-reference/srv-paramnumber-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_setcollen](../../relational-databases/extended-stored-procedures-reference/srv-setcollen-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_paramset](../../relational-databases/extended-stored-procedures-reference/srv-paramset-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_setutype](../../relational-databases/extended-stored-procedures-reference/srv-setutype-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_paramsetoutput](../../relational-databases/extended-stored-procedures-reference/srv-paramsetoutput-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_willconvert](../../relational-databases/extended-stored-procedures-reference/srv-willconvert-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_paramstatus](../../relational-databases/extended-stored-procedures-reference/srv-paramstatus-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
        [srv_wsendmsg](../../relational-databases/extended-stored-procedures-reference/srv-wsendmsg-extended-stored-procedure-api.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [srv_paramtype](../../relational-databases/extended-stored-procedures-reference/srv-paramtype-extended-stored-procedure-api.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
  
