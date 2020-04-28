---
title: 設定唯一的命令 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300838"
---
# <a name="set-unique-command"></a>SET UNIQUE 命令
指定具有重複索引鍵值的記錄是否會在索引檔中維護。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 指定具有重複索引鍵值的任何記錄都不會包含在索引檔案中。 只有具有原始索引鍵值的第一筆記錄才會包含在索引檔案中。  
  
 OFF  
 （預設值）。指定具有重複索引鍵值的記錄會包含在索引檔案中。  
  
## <a name="remarks"></a>備註  
 當您發出重新索引時，索引檔會保留其唯一設定。 如需詳細資訊，請參閱[INDEX](../../odbc/microsoft/index-command.md)。
