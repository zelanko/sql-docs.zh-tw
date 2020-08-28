---
description: Prepared 屬性 (ADO)
title: " (ADO) 的備妥屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
author: rothja
ms.author: jroth
ms.openlocfilehash: 7352d21467061a38bd7e2443ecb52fdb59bd7696
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990039"
---
# <a name="prepared-property-ado"></a>Prepared 屬性 (ADO)
指出是否要在執行之前儲存 [命令](./command-object-ado.md) 的編譯版本。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **布林** 值，如果設定為 **True**，則表示應該準備命令。  
  
## <a name="remarks"></a>備註  
 使用**備**妥的屬性可讓提供者在[命令](./command-object-ado.md)物件第一次執行之前，儲存[CommandText](./commandtext-property-ado.md)屬性中所指定之查詢的備妥 (或編譯的) 版本。 這可能會讓命令的第一次執行變慢，但是一旦提供者編譯命令之後，提供者將會使用命令的編譯版本進行任何後續的執行，這會導致效能提高。  
  
 如果屬性為 **False**，則提供者會直接執行 **命令** 物件，而不會建立編譯的版本。  
  
 如果提供者不支援命令準備，當這個屬性設定為 **True**時，它可能會傳回錯誤。 如果提供者未傳回錯誤，則只會忽略準備命令的要求，並將 **備** 妥的屬性設定為 **False**。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的備妥屬性範例 ](./prepared-property-example-vb.md)   
 [Prepared 屬性範例 (VC++)](./prepared-property-example-vc.md)