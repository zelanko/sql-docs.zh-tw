---
description: 捕獲 ADO 錯誤碼
title: ADO 錯誤碼 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], error codes
ms.assetid: 3aee61c7-a9b7-4596-b78e-5828a00d0281
author: rothja
ms.author: jroth
ms.openlocfilehash: aa933f7be33f564af3aaf2851f6ec32bd5b4c5d4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991179"
---
# <a name="capture-ado-error-codes"></a>捕獲 ADO 錯誤碼
除了[錯誤](../../reference/ado-api/errors-collection-ado.md)集合的[錯誤](../../reference/ado-api/error-object.md)物件中傳回的提供者錯誤，ADO 本身也會將錯誤傳回給執行時間環境的例外狀況處理機制。 使用錯誤捕捉機制的程式設計語言，例如 Microsoft® Visual Basic 中的 **On error** 語句，或 Microsoft Visual C++®中的 **try-catch** 區塊，以捕獲 ADO 錯誤。

 如需 ADO 錯誤碼清單，請參閱 [ErrorValueEnum](../../reference/ado-api/errorvalueenum.md)。

## <a name="see-also"></a>另請參閱
 [ (ADO) 收集](../../reference/ado-api/errors-collection-ado.md)[錯誤物件](../../reference/ado-api/error-object.md)錯誤