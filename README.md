## Introduction

This is a like or star Vue.js component that provides simple sollution for adding and removing likes for your blogs, comments or anything you need.

## Instalation

Add the file LikeComponent.vue to your Vue.js project somewhere among your general components.
You need to install Axios for making Ajax requests and Material design icons, or any other icon pack that provides icons in this way: `<i class=""></i>`.

## Using

Import LikeComponent.vue to a parent component where you want to use it. Use `<LikeComponent \>` or `<like-component></like-component>` tag and add some important attributes like this:<br>
`likeable`: Required. String that specified the name of likeable. For example Article, Comment ...<br>
`likeableId`: Required. Number that specified the id of likeable.<br>
`likesNumber`: Number of likes. Default is 0.<br>
`hasLiked`: Boolean that specified if current user has liked the likeable. Default is False.<br>
`guest`: Boolean that specified if current user is guest. If true, he cannot like anything. Default is False.<br>
`apiUrl`: String that specified the url which is used for Ajax requests. In case user is adding like POST request is send. In opposite case DELETE request is send. Default is '/api/like'.<br>
`likedClass`: String that specified the class of `<i>`element in case the like is added. Default is: 'mdi mdi-star'.<br>
`dontLikedClass`: String that specified the class of `<i>`element in case the like is not added. Default is: 'mdi mdi-star-outline'.<br>

#### Example

You can use this component also outside of parent Vue component. Example usage in Laravel Blade template could look like this:

      `<like-component
      	    likeable="Article"
    	:likeable-id={{ $article->id }}
    	:likes-number={{ $article->likes()->count() }}
    	@auth :has-liked={{ auth()->user()->hasLiked($article) ? 'true' : 'false' }} @endauth
    	@guest :guest="true" @endguest
    >
      </like-component>`
