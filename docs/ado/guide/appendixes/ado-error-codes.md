---
description: 捕獲 ADO 錯誤碼
title: ADO 錯誤碼 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], error codes
ms.assetid: 3aee61c7-a9b7-4596-b78e-5828a00d0281
author: rothja
ms.author: jroth
ms.openlocfilehash: 2502e1dec35ec0d6450190650a18ac765ce14421
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355224"
---
# <a name="capture-ado-error-codes"></a>捕獲 ADO 錯誤碼
除了[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合的[錯誤](../../../ado/reference/ado-api/error-object.md)物件中傳回的提供者錯誤，ADO 本身也會將錯誤傳回給執行時間環境的例外狀況處理機制。 使用錯誤捕捉機制的程式設計語言，例如 Microsoft® Visual Basic 中的 **On error** 語句，或 Microsoft Visual C++®中的 **try-catch** 區塊，以捕獲 ADO 錯誤。

 如需 ADO 錯誤碼清單，請參閱 [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)。

## <a name="see-also"></a>另請參閱
 [ (ADO) 收集](../../../ado/reference/ado-api/errors-collection-ado.md)[錯誤物件](../../../ado/reference/ado-api/error-object.md)錯誤
