<script>
  import BlogContent from "./component/BlogContent.svelte";
  import Documentation from "./component/Documentation.svelte";
  import Product from "./component/Product.svelte";
  import { Router, Route } from "svelte-routing";
</script>

<Router>
  <Route path="/news" component={BlogContent} />
  <Route path="/documentation" component={Documentation} />
  <Route path="/product" component={Product} />
</Router>
