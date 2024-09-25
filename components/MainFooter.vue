<template>
  <div class="main-footer">
    <Container>
      <div class="main-footer__body">
        <div class="main-footer__block">
          <h3>Office Address</h3>
          <div class="main-footer__block-content">
            <div class="main-footer__address">
              <p>
                No.(190/192), Shwe Gone Daing Road, Dagon Tower 8-G, Bahan
                Township, Yangon Region, Myanmar.
              </p>
            </div>
            <div class="main-footer__telephone">
              <div>
                <img src="/image/phone-icon.svg" />
              </div>
              <div>
                <p>
                  <span>09 787 022 000, 09 787 011 000,</span>
                  <span>09 765 681 608, 09 765 681 601</span>
                </p>
              </div>
            </div>
            <div class="main-footer__email">
              <div>
                <img src="/image/email-icon.svg" />
              </div>
              <div>
                <p>saleandmarketing@chemistwarehouse.org</p>
              </div>
            </div>
            <div class="main-footer__social">
              <div>
                <a
                  href="https://www.facebook.com/ChemistWarehouseCompany?mibextid=ZbWKwL"
                  target="_blank"
                >
                  <img src="/assets/svg/facebook.svg" alt="" />
                </a>
              </div>
              <div>
                <a href="https://t.me/ChemistWarhouse" target="_blank">
                  <img src="/assets/svg/telegram.svg" alt="" />
                </a>
              </div>
              <div>
                <a
                  href="https://instagram.com/chemistwarehouseco.ltd?igshid=ZDdkNTZiNTM="
                  target="_blank"
                >
                  <img src="/assets/svg/instagram.svg" alt="" />
                </a>
              </div>
              <div>
                <a
                  href="https://invite.viber.com/?g2=AQBJbkwuklUYS0527aSRXBsWM2iUrSVeVPeeygn1o23Vb%2FHLcQGMl4BA28VzIwOF"
                  target="_blank"
                >
                  <img src="/assets/svg/viber.svg" alt="" />
                </a>
              </div>
            </div>
          </div>
        </div>
        <div class="main-footer__block">
          <h3>Other Address</h3>
          <div class="main-footer__block-content main-footer__other-address">
            <div><a href="">Yangon Shop</a></div>
            <div><a href="">Mawlamyine Shop</a></div>
            <div><a href="">Warehouse 1</a></div>
            <div><a href="">Warehouse 2</a></div>
          </div>
        </div>
        <div class="main-footer__block">
          <h3>Menu</h3>
          <div class="main-footer__block-content main-footer__menu">
            <div>
              <NuxtLink to="/">Home</NuxtLink>
            </div>
            <div>
              <NuxtLink to="/about">About</NuxtLink>
            </div>
            <div>
              <NuxtLink to="/products">Products / Services</NuxtLink>
            </div>
            <div>
              <NuxtLink to="/csr">CSR</NuxtLink>
            </div>
            <div>
              <NuxtLink to="/vacancies">Vacancies</NuxtLink>
            </div>
            <div>
              <NuxtLink to="/contact">Contact</NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </Container>
  </div>
</template>

<style scoped>
.main-footer__body {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10rem;
  padding: 40px 0;
  border-top: 1px solid #d5d5f5;
}

.main-footer__block h3 {
  margin-bottom: 20px;
  font-size: 16px;
  font-weight: 700;
  color: #595959;
}

.main-footer__block-content {
  margin-left: 20px;
}
.main-footer__block-content p,
.main-footer__block-content a {
  font-size: 14px;
  color: #8a8a8a;
  text-decoration: none;
}
.main-footer__block-content a:hover {
  text-decoration: underline;
}

.main-footer__telephone,
.main-footer__email {
  display: flex;
  flex-direction: row;
}
.main-footer__telephone div:first-child,
.main-footer__email div:first-child {
  margin-right: 10px;
}
.main-footer__email {
  align-items: center;
}
.main-footer__address {
  margin-bottom: 10px;
  line-height: 1.5;
}
.main-footer__telephone {
  margin-bottom: 10px;
}
.main-footer__other-address > div,
.main-footer__menu > div {
  margin-bottom: 10px;
}
.main-footer__social {
  margin-top: 10px;
}
.main-footer__social div {
  display: inline-block;
  margin-right: 10px;
}

@media screen and (max-width: 860px) {
  .main-footer__body {
    grid-gap: 2rem;
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
