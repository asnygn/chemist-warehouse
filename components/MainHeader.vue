<script>
export default {
  mounted() {
    const body = document.querySelector("body");
    const burger = document.querySelector(".burger");
    const menu = document.querySelector(".main-menu");
    const overlay =
      document.querySelector(".menu-overlay") || document.createElement("div");
    overlay.classList.add("menu-overlay");
    overlay.classList.remove("menu-overlay--show");

    body.appendChild(overlay);
    body.classList.remove("fixed-position");

    burger.addEventListener("click", () => {
      overlay.classList.toggle("menu-overlay--show");
      body.classList.add("fixed-position");
      menu.classList.toggle("main-menu--active");
      burger.classList.add("burger--toggle");
    });

    overlay.addEventListener("click", function () {
      this.classList.remove("menu-overlay--show");
      menu.classList.remove("main-menu--active");
      body.classList.remove("fixed-position");
      burger.classList.remove("burger--toggle");
    });
  },
};
</script>

<template>
  <div class="main-header">
    <Container>
      <div class="main-header__body">
        <Logo />
        <div class="main-menu">
          <ul>
            <li>
              <NuxtLink to="/">Home</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/about">About</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/products">Products / Services</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/csr">CSR</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/vacancies">Vacancies</NuxtLink>
            </li>
            <li>
              <NuxtLink to="/contact">Contact</NuxtLink>
            </li>
          </ul>
        </div>
        <div class="burger">
          <div class="burger__line1"></div>
          <div class="burger__line2"></div>
          <div class="burger__line3"></div>
        </div>
      </div>
    </Container>
  </div>
</template>

<style scoped>
/* Main Header */
.main-header {
  padding: 20px 0;
  background-color: #fff;
}
.main-header__body {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

/* Main Menu */
.main-menu ul {
  display: flex;
  gap: 35px;
  margin-top: 0;
  margin-bottom: 0;
  padding: 0;
  list-style: none;
}
.main-menu a {
  display: block;
  padding: 5px 0;
  font-size: 16px;
  font-weight: 400;
  color: var(--menu-color);
  text-decoration: none;
  transition: color linear 0.3s;
}
.main-menu a:hover,
.main-menu .router-link-exact-active {
  color: var(--primary-color);
}

/* Burger */
.burger {
  display: none;
}
.burger--toggle .burger__line1 {
  transform: rotate(-45deg) translate(-5px, 6px);
}
.burger--toggle .burger__line2 {
  opacity: 0;
}
.burger--toggle .burger__line3 {
  transform: rotate(45deg) translate(-5px, -6px);
}

@media screen and (max-width: 890px) {
  /* Main Menu */
  .main-menu {
    position: absolute;
    top: 0;
    right: 0;
    width: 50%;
    height: 100%;
    z-index: 100;
    background-color: #222;
    /* transform: translateX(100%); */
    transition: transform 0.3s ease-in;
    display: none;
  }
  .main-menu--active {
    display: block;
    /* transform: translateX(0); */
  }
  .main-menu ul {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    margin-top: 40px;
  }
  .main-menu a {
    color: #fff;
  }
  .main-menu a:hover,
  .main-menu .router-link-exact-active {
    color: #666;
  }

  /* Burger */
  .burger {
    display: block;
    cursor: pointer;
  }
  .burger div {
    width: 25px;
    height: 3px;
    margin: 5px;
    background-color: black;
    transition: all 0.3s ease;
  }
}
</style>
