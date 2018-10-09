---
title: 步驟 1︰設定 PHP 開發的開發環境 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 823177f8fef91dda8cf879f6be84ef6706224fad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600236"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>步驟 1︰設定 Node.js 開發的開發環境
您必須設定您的開發環境的先決條件，才能開發應用程式使用 Node.js Driver for SQL Server。  最常見的方法是使用 node package manager (npm) 安裝冗長乏味的模組，但是您可以下載該冗長乏味的模組，直接在[Github](https://github.com/pekim/tedious)如果您偏好。  
  
請注意，Node.js 驅動程式會使用 TDS 通訊協定，SQL Server 和 Azure SQL Database 中的預設會啟用。  不需要進行其他組態設定。  
  
## <a name="windows"></a>Windows  
  
1. **安裝 Node.js 執行階段和 npm 封裝管理員**  
A. 移至[Node.js](https://nodejs.org/en/download/)  
B. 按一下適當的 Windows 安裝程式 msi 連結。   
c. 下載完成後，執行安裝 Node.js msi  
  
2. **開啟 cmd.exe**  
  
3. **建立專案目錄**並瀏覽至它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **建立節點的專案。**  若要在您的專案建立期間保留預設值，按 enter 鍵之前建立專案。 在這個步驟結束時，您應該會在您的專案目錄中看到 package.json 檔案。  
```  
> npm init  
```  
  
5. **在專案中安裝冗長乏味的模組。**  這是驅動程式會使用與 SQL Server 通訊的 TDS 通訊協定的實作。  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux 17.10  
  
1.  **開啟終端機**  
  
2. **安裝 Node.js 執行階段**  
```  
>sudo apt-get install node  
```  
3. **安裝 npm （節點封裝管理員）**  
```  
> sudo apt-get install npm  
```  
4. **建立專案目錄**並瀏覽至它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **建立節點的專案。**  若要在您的專案建立期間保留預設值，按 enter 鍵之前建立專案。 在這個步驟結束時，您應該會在您的專案目錄中看到 package.json 檔案。  
```  
> sudo npm init  
```  
  
6. **在專案中安裝冗長乏味的模組。**  這是驅動程式會使用與 SQL Server 通訊的 TDS 通訊協定的實作。  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **安裝 Node.js 執行階段和 npm 封裝管理員**  
A. 移至[Node.js](https://nodejs.org/en/download/)  
B. 按一下適當的 Mac OS 安裝程式連結。  
c. 下載完成後，執行安裝 Node.js dmg  
  
2. **開啟終端機**  
  
3. **建立專案目錄**並瀏覽至它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **建立節點的專案。**  若要在您的專案建立期間保留預設值，按 enter 鍵之前建立專案。 在這個步驟結束時，您應該會在您的專案目錄中看到 package.json 檔案。  
```  
> npm init  
```  
  
5. **在專案中安裝冗長乏味的模組。**  這是驅動程式會使用與 SQL Server 通訊的 TDS 通訊協定的實作。  
```  
> npm install tedious  
```  
  
