---
description: SET UNIQUE 命令
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
ms.openlocfilehash: b8fa4ca11ed5beae08bfcbeb8b5a55d6c2969785
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412454"
---
# <a name="set-unique-command"></a>SET UNIQUE 命令
指定是否在索引檔中維護具有重複索引鍵值的記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 指定具有重複索引鍵值的任何記錄都不包含在索引檔案中。 索引檔中只會包含具有原始索引鍵值的第一個記錄。  
  
 OFF  
  (預設值。 ) 指定索引檔中包含重複索引鍵值的記錄。  
  
## <a name="remarks"></a>備註  
 當您發出索引編制索引時，索引檔會保留其設定的唯一設定。 如需詳細資訊，請參閱 [索引](../../odbc/microsoft/index-command.md)。
