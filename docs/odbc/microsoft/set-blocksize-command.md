---
title: SET BLOCKSIZE 命令 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e904d341513047b3940cf5b3fc2ba9538cdb5c8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764226"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 命令
指定附註欄位的儲存體如何配置磁碟空間。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>引數  
 *nBytes*  
 指定附註欄位的磁碟空間可配置的區塊大小。 如果*nBytes*為 0 時，單一位元組 （1 個位元組的區塊） 中配置磁碟空間。 如果*nBytes*是介於 1 到 32，磁碟空間之間的整數會以區塊的配置*nBytes*位元組乘以 512。 如果*nBytes*大於 32，在區塊中配置磁碟空間*nBytes*位元組。 如果您指定的區塊大小值大於 32，您可以節省大量的磁碟空間。  
  
## <a name="remarks"></a>備註  
 設定區塊大小的預設值為 64。 若要建立檔案之後，請重設為不同值的區塊大小，將它設定為新的值，然後使用複製來建立新的資料表。 新的資料表有指定的區塊大小。
