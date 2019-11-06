# actix-web-middleware-redirect-https


[![Build Status](https://travis-ci.org/petertrotman/actix-web-middleware-redirect-https.svg?branch=master)](https://travis-ci.org/petertrotman/actix-web-middleware-redirect-https)

A middleware for actix-web which forwards all `http` requests to `https` with optional url string replacement.

[crates.io](https://crates.io/crates/actix-web-middleware-redirect-https)
[Docs](https://docs.rs/actix-web-middleware-redirect-https)

## Usage

```toml
# Cargo.toml
[dependencies]
actix-web-middleware-redirect-https = "0.1.0"
```

```rust
use actix_web::{ App, web };
use actix_web_middleware_redirect_https::RedirectHTTPS;

App::new()
    .wrap(RedirectHTTPS::default())
    .route("/", web::get().to(|| "Always HTTPS!"));
```
By default, the middleware simply replaces the `scheme` of the URL with `https://`, but you may need to it to change other parts of the URL.
For example, in development if you are not using the default ports (80 and 443) then you will need to specify their replacement, as below:

```rust
use actix_web::{ App, web };
use actix_web_middleware_redirect_https::RedirectHTTPS;

App::new()
    .wrap(RedirectHTTPS::with_replacements(&vec![":8080".to_owned(), ":8443".to_owned()]))
    .route("/", web::get().to(|| "Always HTTPS on non-default ports!"));
```