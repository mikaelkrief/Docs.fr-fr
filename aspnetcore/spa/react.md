---
title: "Utilisez le modèle de projet React"
author: SteveSandersonMS
description: "Découvrez comment démarrer avec le modèle de projet ASP.NET Core seule Page Application (SPA) release candidate pour réagir et application de réagir créer."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/06/2017
ms.devlang: csharp
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: spa/react
ms.openlocfilehash: a63d81633a0f37d24ad5e05de293e3c41004eba1
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2018
---
# <a name="use-the-react-project-template-release-candidate"></a><span data-ttu-id="74403-103">Utilisez le modèle de projet React (version finale)</span><span class="sxs-lookup"><span data-stu-id="74403-103">Use the React project template (release candidate)</span></span>

> [!NOTE]
> <span data-ttu-id="74403-104">Cette documentation n’est pas sur le modèle de projet React finale.</span><span class="sxs-lookup"><span data-stu-id="74403-104">This documentation is not about the released React project template.</span></span> <span data-ttu-id="74403-105">**Cette documentation est sur la version release candidate du modèle React.**</span><span class="sxs-lookup"><span data-stu-id="74403-105">**This documentation is about the release candidate of the React template.**</span></span> <span data-ttu-id="74403-106">Nous espérons qu’expédier la version finale dans 2018 anticipée.</span><span class="sxs-lookup"><span data-stu-id="74403-106">We hope to ship the released version in early 2018.</span></span>

<span data-ttu-id="74403-107">Le modèle de projet React mis à jour fournit un point de départ pratique pour ASP.NET Core des applications à l’aide de réagir et [application react créer](https://github.com/facebookincubator/create-react-app) conventions (ARC) pour implémenter une interface utilisateur côté client riche (IU).</span><span class="sxs-lookup"><span data-stu-id="74403-107">The updated React project template provides a convenient starting point for ASP.NET Core apps using React and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="74403-108">Le modèle est équivalent à la création d’un projet ASP.NET Core pour agir comme un serveur principal d’API et qu’un projet standard arc réagir à agir comme une interface utilisateur, mais avec la commodité d’hébergement à la fois dans un projet d’application unique qui peut être créé et publié comme une unité unique.</span><span class="sxs-lookup"><span data-stu-id="74403-108">The template is equivalent to creating both an ASP.NET Core project to act as an API backend, and a standard CRA React project to act as a UI, but with the convenience of hosting both in a single app project that can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="74403-109">Créer une application</span><span class="sxs-lookup"><span data-stu-id="74403-109">Create a new app</span></span>

<span data-ttu-id="74403-110">Pour commencer, assurez-vous que vous avez [installé le modèle de projet mis à jour React](xref:spa/index#installation).</span><span class="sxs-lookup"><span data-stu-id="74403-110">To get started, ensure you've [installed the updated React project template](xref:spa/index#installation).</span></span> <span data-ttu-id="74403-111">Ces instructions ne s’appliquent pas au modèle de projet précédent React inclus dans le .NET Core 2.0.x SDK.</span><span class="sxs-lookup"><span data-stu-id="74403-111">These instructions don't apply to the previous React project template included in the .NET Core 2.0.x SDK.</span></span>

<span data-ttu-id="74403-112">Créez un nouveau projet à partir d’une invite de commandes à l’aide de la commande `dotnet new react` dans un répertoire vide.</span><span class="sxs-lookup"><span data-stu-id="74403-112">Create a new project from a command prompt using the command `dotnet new react` in an empty directory.</span></span> <span data-ttu-id="74403-113">Par exemple, les commandes suivantes créent l’application dans un *application mon nouveau* active et basculer vers ce répertoire :</span><span class="sxs-lookup"><span data-stu-id="74403-113">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new -o my-new-app
cd my-new-app
```

<span data-ttu-id="74403-114">Exécutez l’application à partir de Visual Studio ou le .NET Core CLI :</span><span class="sxs-lookup"><span data-stu-id="74403-114">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="74403-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74403-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="74403-116">Ouvrez généré *.csproj* , et exécutez l’application normalement à partir de là.</span><span class="sxs-lookup"><span data-stu-id="74403-116">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="74403-117">Le processus de génération restaure npm dépendent de la première exécution, ce qui peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="74403-117">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="74403-118">Les builds suivantes sont beaucoup plus rapides.</span><span class="sxs-lookup"><span data-stu-id="74403-118">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="74403-119">CLI .NET Core</span><span class="sxs-lookup"><span data-stu-id="74403-119">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="74403-120">Assurez-vous d’avoir une variable d’environnement appelée `ASPNETCORE_Environment` avec la valeur `Development`.</span><span class="sxs-lookup"><span data-stu-id="74403-120">Ensure you have an environment variable called `ASPNETCORE_Environment` with value of `Development`.</span></span> <span data-ttu-id="74403-121">Sur Windows (dans les invites de non-PowerShell), exécutez `SET ASPNETCORE_Environment=Development`.</span><span class="sxs-lookup"><span data-stu-id="74403-121">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="74403-122">Sur Linux ou macOS, exécutez `export ASPNETCORE_Environment=Development`.</span><span class="sxs-lookup"><span data-stu-id="74403-122">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="74403-123">Exécutez `dotnet build` pour vérifier votre application se génère correctement.</span><span class="sxs-lookup"><span data-stu-id="74403-123">Run `dotnet build` to verify your app builds correctly.</span></span> <span data-ttu-id="74403-124">Sur la première exécution, le processus de génération restaure les dépendances de npm, qui peuvent prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="74403-124">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="74403-125">Les builds suivantes sont beaucoup plus rapides.</span><span class="sxs-lookup"><span data-stu-id="74403-125">Subsequent builds are much faster.</span></span>

<span data-ttu-id="74403-126">Exécutez `dotnet run` pour démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="74403-126">Run `dotnet run` to start the app.</span></span>

---

<span data-ttu-id="74403-127">Le modèle de projet crée une application ASP.NET Core et une application de réagir.</span><span class="sxs-lookup"><span data-stu-id="74403-127">The project template creates an ASP.NET Core app and a React app.</span></span> <span data-ttu-id="74403-128">L’application ASP.NET Core est destinée à être utilisé pour l’accès aux données, l’autorisation et autres problèmes côté serveur.</span><span class="sxs-lookup"><span data-stu-id="74403-128">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="74403-129">L’application de réagir résidant dans le *ClientApp* sous-répertoire, est destiné à être utilisé pour tous les problèmes de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="74403-129">The React app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="74403-130">Ajouter des pages, les images, les styles, les modules, etc.</span><span class="sxs-lookup"><span data-stu-id="74403-130">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="74403-131">Le *ClientApp* active est une application de réagir de l’arc standard.</span><span class="sxs-lookup"><span data-stu-id="74403-131">The *ClientApp* directory is a standard CRA React app.</span></span> <span data-ttu-id="74403-132">Consultez officielle [documentation de l’arc](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="74403-132">See the official [CRA documentation](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) for more information.</span></span>

<span data-ttu-id="74403-133">Il existe de légères différences entre l’application de réagir créés par ce modèle et celui créé par arc lui-même ; Toutefois, les fonctionnalités de l’application sont identiques.</span><span class="sxs-lookup"><span data-stu-id="74403-133">There are slight differences between the React app created by this template and the one created by CRA itself; however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="74403-134">L’application créée par le modèle contient un [Bootstrap](https://getbootstrap.com/)-en fonction de la mise en page et un exemple de routage de base.</span><span class="sxs-lookup"><span data-stu-id="74403-134">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="74403-135">Installer les packages npm</span><span class="sxs-lookup"><span data-stu-id="74403-135">Install npm packages</span></span>

<span data-ttu-id="74403-136">Pour installer des packages tiers npm, utilisez une invite de commandes dans le *ClientApp* sous-répertoire.</span><span class="sxs-lookup"><span data-stu-id="74403-136">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="74403-137">Exemple :</span><span class="sxs-lookup"><span data-stu-id="74403-137">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="74403-138">Publier et déployer</span><span class="sxs-lookup"><span data-stu-id="74403-138">Publish and deploy</span></span>

<span data-ttu-id="74403-139">Dans le développement, l’application s’exécute en mode optimisé pour des raisons pratiques de développement.</span><span class="sxs-lookup"><span data-stu-id="74403-139">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="74403-140">Par exemple, JavaScript offres incluent des mappages de sources (de sorte que lors du débogage, vous pouvez voir votre code source d’origine).</span><span class="sxs-lookup"><span data-stu-id="74403-140">For example, JavaScript bundles include source maps (so that when debugging, you can see your original source code).</span></span> <span data-ttu-id="74403-141">L’application surveille JavaScript, HTML et CSS de modifications de fichiers sur disque et automatiquement recompile et recharge lorsqu’il rencontre ces fichiers modifier.</span><span class="sxs-lookup"><span data-stu-id="74403-141">The app watches JavaScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="74403-142">Dans la production, ont une version de votre application qui est optimisée pour les performances.</span><span class="sxs-lookup"><span data-stu-id="74403-142">In production, serve a version of your app that is optimized for performance.</span></span> <span data-ttu-id="74403-143">Il est configuré pour se produire automatiquement.</span><span class="sxs-lookup"><span data-stu-id="74403-143">This is configured to happen automatically.</span></span> <span data-ttu-id="74403-144">Lorsque vous publiez, la configuration de build émet une build transpiled réduite, de votre code côté client.</span><span class="sxs-lookup"><span data-stu-id="74403-144">When you publish, the build configuration emits a minified, transpiled build of your client-side code.</span></span> <span data-ttu-id="74403-145">Contrairement à la version de développement, la build de production ne requiert pas Node.js être installé sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="74403-145">Unlike the development build, the production build doesn't require Node.js to be installed on the server.</span></span>

<span data-ttu-id="74403-146">Vous pouvez utiliser standard [méthodes de déploiement et d’hébergement ASP.NET Core](xref:host-and-deploy/index).</span><span class="sxs-lookup"><span data-stu-id="74403-146">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-the-cra-server-independently"></a><span data-ttu-id="74403-147">Exécuter le serveur de l’arc indépendamment</span><span class="sxs-lookup"><span data-stu-id="74403-147">Run the CRA server independently</span></span>

<span data-ttu-id="74403-148">Le projet est configuré pour démarrer sa propre instance du serveur de développement arc en arrière-plan lorsque l’application ASP.NET Core démarre en mode de développement.</span><span class="sxs-lookup"><span data-stu-id="74403-148">The project is configured to start its own instance of the CRA development server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="74403-149">Ceci est pratique car elle signifie que vous n’êtes pas obligé d’exécuter un serveur distinct manuellement.</span><span class="sxs-lookup"><span data-stu-id="74403-149">This is convenient because it means you don't have to run a separate server manually.</span></span>

<span data-ttu-id="74403-150">Il existe un inconvénient de ce programme d’installation par défaut.</span><span class="sxs-lookup"><span data-stu-id="74403-150">There is a drawback to this default setup.</span></span> <span data-ttu-id="74403-151">Chaque fois que vous modifiez votre code c# et base ASP.NET application doit redémarrer, le serveur de l’arc redémarre.</span><span class="sxs-lookup"><span data-stu-id="74403-151">Each time you modify your C# code and your ASP.NET Core app needs to restart, the CRA server restarts.</span></span> <span data-ttu-id="74403-152">Quelques secondes sont requises pour démarrer la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="74403-152">A few seconds are required to start back up.</span></span> <span data-ttu-id="74403-153">Si vous apportez des modifications de code c# fréquentes et que vous ne souhaitez pas attendre que le serveur de l’arc à redémarrer, exécutez le serveur d’arc en externe, indépendamment du processus ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="74403-153">If you're making frequent C# code edits and don't want to wait for the CRA server to restart, run the CRA server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="74403-154">Pour cela :</span><span class="sxs-lookup"><span data-stu-id="74403-154">To do so:</span></span>

1. <span data-ttu-id="74403-155">Dans une invite de commandes, basculez vers le *ClientApp* sous-répertoire et lancer le serveur de développement arc :</span><span class="sxs-lookup"><span data-stu-id="74403-155">In a command prompt, switch to the *ClientApp* subdirectory, and launch the CRA development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

2. <span data-ttu-id="74403-156">Modifiez votre application ASP.NET Core pour utiliser l’instance de serveur arc externe au lieu de lancer un de ses propres.</span><span class="sxs-lookup"><span data-stu-id="74403-156">Modify your ASP.NET Core app to use the external CRA server instance instead of launching one of its own.</span></span> <span data-ttu-id="74403-157">Dans votre *démarrage* de classe, remplacez le `spa.UseReactDevelopmentServer` invocation avec les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="74403-157">In your *Startup* class, replace the `spa.UseReactDevelopmentServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

<span data-ttu-id="74403-158">Lorsque vous démarrez votre application ASP.NET Core, il ne sera pas lancer un serveur de l’arc.</span><span class="sxs-lookup"><span data-stu-id="74403-158">When you start your ASP.NET Core app, it won't launch a CRA server.</span></span> <span data-ttu-id="74403-159">L’instance que vous avez démarré manuellement est utilisé à la place.</span><span class="sxs-lookup"><span data-stu-id="74403-159">The instance you started manually is used instead.</span></span> <span data-ttu-id="74403-160">Cela lui permet de démarrer et redémarrer plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="74403-160">This enables it to start and restart faster.</span></span> <span data-ttu-id="74403-161">Il n’attend plus pour votre application de réagir à reconstruire chaque fois.</span><span class="sxs-lookup"><span data-stu-id="74403-161">It's no longer waiting for your React app to rebuild each time.</span></span>