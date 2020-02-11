---
title: 設定區塊命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4fe84a470f5e877c73701168394cd85d75253fb7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997756"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 命令
指定如何配置磁碟空間給備忘欄位的儲存。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>引數  
 *nBytes*  
 指定用來配置備忘欄位之磁碟空間的區塊大小。 如果*nBytes*為0，則會以單一位元組（1個位元組的區塊）配置磁碟空間。 如果*nBytes*是介於1到32之間的整數，則會在*nBytes*位元組的區塊中配置磁碟空間乘以512。 如果*nBytes*大於32，則會在*nBytes*位元組區塊中配置磁碟空間。 如果您指定的區塊大小值大於32，則可以節省大量的磁碟空間。  
  
## <a name="remarks"></a>備註  
 SET 區塊的預設值是64。 若要在建立檔案之後，將區塊大小重設為不同的值，請將它設定為新的值，然後使用 [複製] 來建立新的資料表。 新的資料表具有指定的區塊大小。
