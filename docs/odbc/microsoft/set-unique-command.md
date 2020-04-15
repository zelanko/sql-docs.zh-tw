---
title: 設定獨立命令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d3d37509450d1305891100b37bfd1ad026166e8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300838"
---
# <a name="set-unique-command"></a>SET UNIQUE 命令
指定索引檔中是否保留具有重複索引鍵值的記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 指定索引檔中不包括任何具有重複索引鍵值的記錄。 索引檔中僅包含具有原始索引鍵值的第一個記錄。  
  
 OFF  
 (預設值。指定索引檔中包含具有重複索引鍵值的記錄。  
  
## <a name="remarks"></a>備註  
 當您發出 REINDEX 時,索引檔將保留其"設置唯一"設置。 有關詳細資訊,請參閱[INDEX](../../odbc/microsoft/index-command.md)。
