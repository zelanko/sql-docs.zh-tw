---
title: 設定區塊大小指令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3eb9fbe9df90f7ddafebc6baa029164a578a6da3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300898"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 命令
指定如何為備忘錄欄位的儲存分配磁碟空間。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>引數  
 *n 位元組*  
 指定分配備忘錄欄位的磁碟空間的塊大小。 如果*n 位元組*為 0,則以單個字節(1 位元組的塊)分配磁碟空間。 如果*n 位元組*是介於 1 和 32 之間的整數,則磁碟空間以 n*位元組*乘以 512 為單位分配。 如果*n 位元組*大於 32,則以 n*位元組*塊分配磁碟空間。 如果指定塊大小值大於 32,則可以節省大量磁碟空間。  
  
## <a name="remarks"></a>備註  
 SET BLOCKSIZE 的預設值為 64。 要在創建檔後將塊大小重置為其他值,請將其設置為新值,然後使用 COPY 創建新表。 新表具有指定的塊大小。
