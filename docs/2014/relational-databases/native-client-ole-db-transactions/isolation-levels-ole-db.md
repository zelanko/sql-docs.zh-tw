---
title: 隔離等級 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4026154204cf6de95711a3014b069c34a29d9922
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704515"
---
# <a name="isolation-levels-ole-db"></a>隔離等級 (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端可以控制連線的交易隔離等級。 若要控制交易隔離等級， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者會使用：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者預設自動認可模式的 DBPROPSET_SESSION 屬性 DBPROP_SESS_AUTOCOMMITISOLEVELS。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]層級的 Native Client OLE DB 提供者預設值為 DBPROPVAL_TI_READCOMMITTED。  
  
-   適用於本機手動認可交易之 **ITransactionLocal::StartTransaction** 方法的 *isoLevel* 參數。  
  
-   適用於 MS DTC 協調分散式交易之 **ITransactionDispenser::BeginTransaction** 方法的 *isoLevel* 參數。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許中途讀取隔離等級的唯讀存取。 其他所有等級藉由將鎖定套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件以限制並行存取。 由於用戶端需要更高的並行存取等級，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會對資料並行存取套用更大的限制。 為了維持最高層級的資料平行存取， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者應該以智慧方式控制它對特定並行層級的要求。  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 引入了快照集隔離等級。 如需詳細資訊，請參閱[使用快照隔離](../native-client/features/working-with-snapshot-isolation.md)。  
  
## <a name="see-also"></a>另請參閱  
 [交易](transactions.md)  
  
  
