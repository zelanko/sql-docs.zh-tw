---
title: "步驟 1： 設定適用於 Node.js 開發的開發環境 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b4e41033ffb30801fd388f7816c34c8a7751daa9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>步驟 1： 設定適用於 Node.js 開發的開發環境
您必須設定開發環境的必要條件，才能開發使用 Node.js Driver for SQL Server 的應用程式。  最常見的方法是使用 node 封裝管理員 (npm) 安裝冗長的模組，但是您可以下載冗長的模組，直接在[Github](https://github.com/pekim/tedious)如果您偏好。  
  
請注意 Node.js 驅動程式會使用 TDS 通訊協定，SQL Server 和 Azure SQL Database 中的預設會啟用。  不需要進行其他組態設定。  
  
## <a name="windows"></a>Windows  
  
1. **安裝 Node.js 執行階段及 npm 封裝管理員**  
a. 移至[Node.js](https://nodejs.org/en/download/)  
b. 按一下適當的 Windows 安裝程式 msi 連結。   
c. 在下載後，執行 msi 安裝 Node.js  
  
2. **開啟 cmd.exe**  
  
3. **建立專案目錄**並瀏覽到它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **建立節點的專案。**  若要在專案建立期間保留預設值，按 enter 鍵直到建立專案。 在這個步驟結束時，您應該會在您的專案目錄中看到 package.json 檔案。  
```  
> npm init  
```  
  
5. **您的專案中安裝冗長的模組。**  這是與 SQL Server 進行通訊的驅動程式會使用 TDS 通訊協定的實作。  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **開啟終端機**  
  
2. **安裝 Node.js 執行階段**  
```  
>sudo apt-get install node  
```  
3. **安裝 npm （node 封裝管理員）**  
```  
> sudo apt-get install npm  
```  
4. **建立專案目錄**並瀏覽到它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **建立節點的專案。**  若要在專案建立期間保留預設值，按 enter 鍵直到建立專案。 在這個步驟結束時，您應該會在您的專案目錄中看到 package.json 檔案。  
```  
> sudo npm init  
```  
  
6. **您的專案中安裝冗長的模組。**  這是與 SQL Server 進行通訊的驅動程式會使用 TDS 通訊協定的實作。  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **安裝 Node.js 執行階段及 npm 封裝管理員**  
a. 移至[Node.js](https://nodejs.org/en/download/)  
b. 按一下適當的 Mac OS 安裝程式連結。  
c. 在下載後，執行安裝 Node.js dmg  
  
2. **開啟終端機**  
  
3. **建立專案目錄**並瀏覽到它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **建立節點的專案。**  若要在專案建立期間保留預設值，按 enter 鍵直到建立專案。 在這個步驟結束時，您應該會在您的專案目錄中看到 package.json 檔案。  
```  
> npm init  
```  
  
5. **您的專案中安裝冗長的模組。**  這是與 SQL Server 進行通訊的驅動程式會使用 TDS 通訊協定的實作。  
```  
> npm install tedious  
```  
  

