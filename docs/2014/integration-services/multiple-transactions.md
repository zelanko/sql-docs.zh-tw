---
title: 多個交易 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], multiple
- multiple transactions
ms.assetid: c3664a94-be89-40c0-a3a0-84b74a7fedbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1c922fb612faca72e9f9381990dc777301185cb1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176578"
---
# <a name="multiple-transactions"></a>多個交易
  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝中，封裝可以包含不相關的交易。 任何時候如果巢狀容器階層中間的容器不支援交易，而階層中其上面或下面的容器設定為支援交易，則這些容器就會啟動分別的交易。 交易會從巢狀容器階層中最內層的工作到封裝依序進行認可或回復。 不過，內部交易認可後，如果外部交易已中止，則不會回復該交易。

## <a name="illustration-of-multiple-transactions"></a>多個交易的圖例
 例如，封裝具有的「時序」容器包含兩個「Foreach 迴圈」容器，而每個容器包含兩個「執行 SQL」工作。 時序容器支援交易，Foreach 迴圈容器不支援，而執行 SQL 工作則支援。 在此範例中，每一個執行 SQL 工作都會啟動自己的交易，而即使時序工作上的交易中止，也不會回復。

 「時序」容器、「Foreach 迴圈」容器和「執行 SQL」工作的 TransactionOption 屬性設定如下：

-   「時序」容器的 TransactionOption 屬性會設為 **Required**。

-   「Foreach 迴圈」容器的 TransactionOption 屬性會設為 **NotSupported**。

-   「執行 SQL」工作的 TransactionOption 屬性會設為 **Required**。

 下圖顯示封裝中五個不相關的交易。 一個交易是由「時序」容器啟動的，四個交易是由「執行 SQL」工作啟動的。

 ![多個交易的實作](media/mw-dts-trans2.gif "多個交易的實作")

## <a name="related-tasks"></a>相關工作
 [設定封裝來使用交易](../relational-databases/native-client-ole-db-transactions/transactions.md)


