---
date: 2009-04-28 11:30:00
layout: post
redirect_from: "post/2009/04/28/Pinguer-une-Url"
tags: code-snippets, c-sharp
title: "Pinguer une Url"
---

Il est quelquefois très pratique de pouvoir exécuter un traitement sur un
site web. Par exemple, dans PI il existe une page pour sauvegarder
automatiquement la base de données. Le problème, c'est que sous Windows, il
n'est pas possible de faire une tache planifiée qui appelle directement une
page web.

J'avais écrit il y a quelques temps un petit utilitaire UrlPing pour faire
une requête sur une page web en indiquant simplement l'url à atteindre. Tout
marchait plutôt bien depuis plus d'un an jusqu'à ce qu'hier j'essaie de
l'utiliser avec une url qui ne correspond pas à un "vrai" fichier .aspx mais à
une url "rewritée". Et là, cela provoque une erreur du type "[Tentatives de redirection
automatique trop nombreuses](http://stackoverflow.com/questions/518181/too-many-automatic-redirections-were-attempted-error-message-when-using-a-httpweb)".

J'en ai donc profité pour améliorer le code et le publier si jamais cela
intéresse quelqu'un.

```
namespace Altrr.Tools.UrlPing {

  using System;
  using System.Net;

  class Start {

    [STAThread]
    static void Main(string[] args) {

      if (args.Length == 1) {
        string url = args[0];
        Console.Write(url + " : ");
        try {
          HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(url);
          request.CookieContainer = new CookieContainer();
          request.Method = "HEAD";
          HttpWebResponse response = (HttpWebResponse)request.GetResponse();
          Console.WriteLine("OK (" + Convert.ToInt32(response.StatusCode) + " - " + response.StatusDescription + ")");
          string urlr = response.ResponseUri.ToString();
          if (url != urlr) {
            Console.WriteLine("-------
" + urlr);
          }
        } catch (Exception ex) {
          Console.WriteLine("KO
-------
" + ex.Message);
        }
      } else {
        Console.WriteLine("Syntax : UrlPing url");
      }

    }

  }
}
```
