<script>
    import Simulation from "./Simulation.svelte";
    import router from "page";
    import routes from "./routes";

    let page = null;
    let params = {};
    let user = true;
    routes.forEach((route) => {
        router(
            route.path,
            (ctx, next) => {
                params = { ...ctx.params };
                next();
            },
            () => {
                if (route.auth && !user) {
                    router.redirect("/");
                } else {
                    page = route.component;
                }
            }
        );
    });
    router.start();
</script>

<main>
    <svelte:component this={page} {params} />
  </main>