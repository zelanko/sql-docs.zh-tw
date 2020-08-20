---
description: SET BLOCKSIZE 命令
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6677a397542f4bcd7f27b11cd032092b7087a9fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466390"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 命令
指定如何配置磁碟空間來儲存備註欄位。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>引數  
 *n*  
 指定配置備註欄位之磁碟空間的區塊大小。 如果 *n* 為0，則會以單一位元組配置磁碟空間， (1 位元組) 的區塊。 如果 *n* 是介於1到32之間的整數，則會在 *n* 位元組乘以512的區塊中配置磁碟空間。 如果 *n* 大於32，則會以 *n* 位元組區塊配置磁碟空間。 如果您指定的區塊大小值大於32，則可以節省大量的磁碟空間。  
  
## <a name="remarks"></a>備註  
 SET 區塊集的預設值是64。 若要在建立檔案之後，將區塊大小重設為不同的值，請將它設定為新的值，然後使用 [複製] 來建立新的資料表。 新的資料表具有指定的區塊大小。
