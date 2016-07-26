# Laravel note

### Use `Eloquent`'s `scope` __BEFORE__ raw quries.
* version: 5.2

>
You can specify `scope` in your eloquent model to make custom query more clearlify,   
however, if you use `scope` function __AFTER__ after raw eloquent query like `where`,   
_all_ raw eloquent queries will be removed from the real mysql query excuted by laravel.
