<script>
  import { Router, links, Route } from "svelte-routing";
  import {
    Header,
    HeaderNav,
    HeaderNavItem,
    SideNav,
    SideNavItems,
    SideNavLink,
    SkipToContent,
    Content,
    InlineNotification,
  } from "carbon-components-svelte";

  import Home from "./routes/Home.svelte";
  import About from "./routes/About.svelte";

  let isSideNavOpen = false;
</script>

<!--  -->
<div use:links>
  <Router url="">
    <Header
      company="My"
      platformName="App"
      bind:isSideNavOpen
      expandedByDefault={false}
    >
      <div slot="skip-to-content">
        <SkipToContent />
      </div>

      <HeaderNav>
        <HeaderNavItem text="Home" href="/" />
        <HeaderNavItem text="About" href="/about" />
      </HeaderNav>

      <SideNav bind:isOpen={isSideNavOpen}>
        <SideNavItems>
          <SideNavLink
            text="Home"
            href="/"
            on:click={() => (isSideNavOpen = !isSideNavOpen)}
          />
          <SideNavLink
            text="About"
            href="/about"
            on:click={() => (isSideNavOpen = !isSideNavOpen)}
          />
        </SideNavItems>
      </SideNav>
    </Header>

    <Content>
      <Route path="/" component={Home} />
      <Route path="/about" component={About} />
      <Route let:location>
        <InlineNotification
          hideCloseButton
          title="Error:"
          subtitle={`No route found for ${location.pathname}`}
        />
      </Route>
    </Content>
  </Router>
</div>
