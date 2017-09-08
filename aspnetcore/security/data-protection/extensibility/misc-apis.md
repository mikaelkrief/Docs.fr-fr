---
title: API diverses
author: rick-anderson
description: 
keywords: ASP.NET Core,
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 512c6ba7-88ec-47e4-a656-6b30350b34e6
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/extensibility/misc-apis
ms.openlocfilehash: 541dd721a00495632f0d633577b55933c9be03fa
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2017
---
# <a name="miscellaneous-apis"></a><span data-ttu-id="77824-103">API diverses</span><span class="sxs-lookup"><span data-stu-id="77824-103">Miscellaneous APIs</span></span>

<a name=data-protection-extensibility-mics-apis></a>

>[!WARNING]
> <span data-ttu-id="77824-104">Les types qui implémentent des interfaces suivantes doivent être thread-safe pour les appelants plusieurs.</span><span class="sxs-lookup"><span data-stu-id="77824-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

## <a name="isecret"></a><span data-ttu-id="77824-105">ISecret</span><span class="sxs-lookup"><span data-stu-id="77824-105">ISecret</span></span>

<span data-ttu-id="77824-106">L’interface ISecret représente une valeur secrète, tels que du matériel de clé de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="77824-106">The ISecret interface represents a secret value, such as cryptographic key material.</span></span> <span data-ttu-id="77824-107">Il contient la surface API suivante.</span><span class="sxs-lookup"><span data-stu-id="77824-107">It contains the following API surface.</span></span>

* <span data-ttu-id="77824-108">Longueur : int</span><span class="sxs-lookup"><span data-stu-id="77824-108">Length : int</span></span>

* <span data-ttu-id="77824-109">Dispose() : void</span><span class="sxs-lookup"><span data-stu-id="77824-109">Dispose() : void</span></span>

* <span data-ttu-id="77824-110">WriteSecretIntoBuffer (ArraySegment<byte> tampon) : void</span><span class="sxs-lookup"><span data-stu-id="77824-110">WriteSecretIntoBuffer(ArraySegment<byte> buffer) : void</span></span>

<span data-ttu-id="77824-111">La méthode WriteSecretIntoBuffer remplit la mémoire tampon fournie avec la valeur brute de secret principal.</span><span class="sxs-lookup"><span data-stu-id="77824-111">The WriteSecretIntoBuffer method populates the supplied buffer with the raw secret value.</span></span> <span data-ttu-id="77824-112">La raison de que cette API prend la mémoire tampon comme un paramètre au lieu de retourner qu'un byte [] est directement que cela permet l’appelant pour épingler l’objet de la mémoire tampon, limiter l’exposition de secret principal pour le RÉCUPÉRATEUR de mémoire managée.</span><span class="sxs-lookup"><span data-stu-id="77824-112">The reason this API takes the buffer as a parameter rather than returning a byte[] directly is that this gives the caller the opportunity to pin the buffer object, limiting secret exposure to the managed garbage collector.</span></span>

<span data-ttu-id="77824-113">Le type de secret principal est une implémentation concrète de ISecret où la valeur secrète est stockée dans la mémoire d’en cours.</span><span class="sxs-lookup"><span data-stu-id="77824-113">The Secret type is a concrete implementation of ISecret where the secret value is stored in in-process memory.</span></span> <span data-ttu-id="77824-114">Sur les plateformes Windows, la valeur de clé secrète est chiffrée [CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="77824-114">On Windows platforms, the secret value is encrypted via [CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx).</span></span>