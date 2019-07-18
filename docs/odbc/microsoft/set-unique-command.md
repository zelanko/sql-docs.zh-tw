---
title: SET UNIQUE 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29598ed97cba8be04a0c08727cffc40e663becba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063608"
---
# <a name="set-unique-command"></a>SET UNIQUE 命令
指定是否要將具有重複的索引鍵值的記錄維持索引檔案中。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 ON  
 指定在索引檔案，都不包含任何重複的索引鍵值的記錄。 只有原始索引鍵值的第一個記錄包含在索引檔案。  
  
 OFF  
 （預設值）。指定在索引檔案中包含重複的索引鍵值的記錄。  
  
## <a name="remarks"></a>備註  
 當您發出重新索引時，索引檔仍會保留其設定唯一的設定。 如需詳細資訊，請參閱 < [INDEX](../../odbc/microsoft/index-command.md)。
