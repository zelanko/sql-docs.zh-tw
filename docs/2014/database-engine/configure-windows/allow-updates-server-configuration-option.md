---
title: allow updates 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- allow updates option
ms.assetid: 3967c3ed-280a-4de8-a2ce-393e82745a7b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d7e3ede317509a2044be90635db46e30a932af66
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935909"
---
# <a name="allow-updates-server-configuration-option"></a>允許更新伺服器組態選項
  此選項仍會出現在 **sp_configure** 預存程序中，但其功能已無法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中使用。 此設定無效。 不支援對系統資料表的直接更新。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 變更 **allow updates** 選項將會導致 RECONFIGURE 陳述式失敗。 應該從所有指令碼移除對於 **allow updates** 選項的變更。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
