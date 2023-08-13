# Unable to get typecheck working for hydrogen in turborepo

## How this repository is setup
This is just the kitchen-sink turborepo example with a hydrogen storefront added to it using `npm create @shopify/hydrogen@latest`

## Steps to reproduce

1. Clone this repository
2. Run `yarn install`
3. Run `yarn typecheck`

The following type errors show up. These are **NOT** present if you setup the storefront in a standalone repository.

```
app/root.tsx:92:10 - error TS2739: Type '{ children: Element; data: SerializeObject<UndefinedToOptional<{ cart: Promise<Cart | null>; footer: Promise<FooterQuery>; header: HeaderQuery; isLoggedIn: boolean; publicStoreDomain: string; }>>; [typedDeferredDataBrand]: "TypedDeferredData"; init?: SerializeObject<...> | undefined; }' is missing the following properties from type 'LayoutProps': cart, footer, header, isLoggedIn

92         <Layout {...data}>
            ~~~~~~

app/routes/($locale)._index.tsx:28:44 - error TS2339: Property 'featuredCollection' does not exist on type 'SerializeObject<UndefinedToOptional<Pick<DeferredData, "init"> & { data: { featuredCollection: Pick<Collection, "id" | "handle" | "title"> & { image?: Maybe<Pick<Image, "id" | ... 3 more ... | "height">> | undefined; }; recommendedProducts: Promise<...>; }; readonly [typedDeferredDataBrand]: "TypedDeferredData"; }>>'.

28       <FeaturedCollection collection={data.featuredCollection} />
                                              ~~~~~~~~~~~~~~~~~~

app/routes/($locale)._index.tsx:29:43 - error TS2339: Property 'recommendedProducts' does not exist on type 'SerializeObject<UndefinedToOptional<Pick<DeferredData, "init"> & { data: { featuredCollection: Pick<Collection, "id" | "handle" | "title"> & { image?: Maybe<Pick<Image, "id" | ... 3 more ... | "height">> | undefined; }; recommendedProducts: Promise<...>; }; readonly [typedDeferredDataBrand]: "TypedDeferredData"; }>>'.

29       <RecommendedProducts products={data.recommendedProducts} />
                                             ~~~~~~~~~~~~~~~~~~~

app/routes/($locale).products.$handle.tsx:106:10 - error TS2339: Property 'product' does not exist on type 'SerializeObject<UndefinedToOptional<TypedDeferredData<{ product: Pick<Product, "id" | "handle" | "title" | "description" | "vendor" | "descriptionHtml"> & { options: Pick<ProductOption, "name" | "values">[]; selectedVariant?: Maybe<...> | undefined; variants: { ...; }; seo: Pick<...>; }; variants: Promise<...>; }>>>'.

106   const {product, variants} = useLoaderData<typeof loader>();
             ~~~~~~~

app/routes/($locale).products.$handle.tsx:106:19 - error TS2339: Property 'variants' does not exist on type 'SerializeObject<UndefinedToOptional<TypedDeferredData<{ product: Pick<Product, "id" | "handle" | "title" | "description" | "vendor" | "descriptionHtml"> & { options: Pick<ProductOption, "name" | "values">[]; selectedVariant?: Maybe<...> | undefined; variants: { ...; }; seo: Pick<...>; }; variants: Promise<...>; }>>>'.

106   const {product, variants} = useLoaderData<typeof loader>();
                      ~~~~~~~~

app/routes/($locale).search.tsx:49:10 - error TS2339: Property 'searchTerm' does not exist on type 'SerializeObject<UndefinedToOptional<TypedDeferredData<{ searchTerm: string; searchResults: { results: SearchQuery; totalResults: number; }; }>>> | SerializeObject<...>'.

49   const {searchTerm, searchResults} = useLoaderData<typeof loader>();
            ~~~~~~~~~~

app/routes/($locale).search.tsx:49:22 - error TS2339: Property 'searchResults' does not exist on type 'SerializeObject<UndefinedToOptional<TypedDeferredData<{ searchTerm: string; searchResults: { results: SearchQuery; totalResults: number; }; }>>> | SerializeObject<...>'.

49   const {searchTerm, searchResults} = useLoaderData<typeof loader>();
                        ~~~~~~~~~~~~~


Found 7 errors in 4 files.

Errors  Files
     1  app/root.tsx:92
     2  app/routes/($locale)._index.tsx:28
     2  app/routes/($locale).products.$handle.tsx:106
     2  app/routes/($locale).search.tsx:49
error Command failed with exit code 2.
```