<!-- //head navbar -->

<script>
import { RouterLink } from "vue-router";
import { mapActions } from "vuex";
import axios from "axios";

export default {
  data() {
    return {
      searchKeyword: "",
      cartTotalQuantity: "",
      isUserLoggedIn: sessionStorage.getItem("loggedIn") === "TRUE",
    };
  },

  methods: {
    ...mapActions("search", ["searchProduct"]),
    handleSearch() {
      // 调用搜索方法
      this.searchProduct(this.searchKeyword);
    },
    scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: "smooth", // 平滑滾動效果
      });
    },
    logoutUser() {
      axios
        .post("http://localhost:8080/user/logout")
        .then((response) => {
          // 清除前端的用户状态
          sessionStorage.removeItem("loggedIn");
          sessionStorage.removeItem("user_Id");
          alert("登出");
          this.$router.push("/UserPage/loginPage").then(() => {
            window.location.reload();
          });
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
  computed: {
    isLoggedIn() {
      return this.isUserLoggedIn;
    },
    hasSomeData() {
      return sessionStorage.getItem("someData");
    },
  },

  components: {
    RouterLink,
  },
};
</script>
<template>
  <div class="askUserPage">
    <img src="../views/askAllPage/askHome.vue" alt="" />

    <div class="headerfirst">
      <div class="POP">
      
      </div>
      <div>
        <div>
          <button class="btn" @click="logoutUser" v-if="isLoggedIn">
            登出
          </button>
          <RouterLink class="btn" v-if="isLoggedIn" to="/UserPage/actionShop">
            <i class="fa-solid fa-store"></i> 我的拍賣
          </RouterLink>
          <RouterLink class="btn" v-if="isLoggedIn" to="/UserPage/memberInfo">
            <i class="fa-solid fa-user usericon"></i> 會員資料
          </RouterLink>

          <RouterLink v-if="!isLoggedIn" class="btn" to="/UserPage/loginPage">
            <i class="fa-solid fa-user usericon"></i> 會員登入
          </RouterLink>
        </div>
      </div>
    </div>

    <div class="askHeader">
      <RouterLink class="btn" to="/">
        <h1>
          <i class="fa-solid fa-shrimp"><b> 呱皮皮蝦</b> </i>
        </h1>
      </RouterLink>

      <div class="search-container">
        <input v-model="searchKeyword" placeholder="搜尋" />
        <button @click="handleSearch">搜尋</button>
      </div>

      <div>
        <RouterLink class="btn" to="/UserPage/buyingList">
          <i class="fa-solid fa-box"></i> 購買清單</RouterLink
        >
      </div>

      <div>
        <RouterLink class="btn" to="/UserPage/loginPage"
          ><i class="fa-regular fa-message"></i> 聊聊訊息</RouterLink
        >
      </div>
      <div>
        <RouterLink class="btn" to="/UserPage/shoppingCart">
          <i class="fa-solid fa-cart-shopping usericon"></i>購物車
          <span class="notification-badge">{{ cartTotalQuantity }}</span>
        </RouterLink>
      </div>
    </div>
  </div>
  <div class="Marquee">
    <div class="announcement">
      <p>負責人廖董事長感謝您的加入！！</p>
    </div>

    <!-- 產品分類下拉式選單 -->
    <div class="type">
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item dropdown">
                <a
                  class="nav-link dropdown-toggle"
                  href="#"
                  id="navbarDropdown"
                  role="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                  data-bs-auto-close="false"
                >
                  產品分類
                </a>
                <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                  <div class="accordion" id="accordionExample">
                    <div class="accordion-item">
                      <h2 class="accordion-header" id="headingOne">
                        <button
                          class="accordion-button"
                          type="button"
                          data-bs-toggle="collapse"
                          data-bs-target="#collapseOne"
                          aria-expanded="true"
                          aria-controls="collapseOne"
                        >
                          食品專區
                        </button>
                      </h2>
                      <div
                        id="collapseOne"
                        class="accordion-collapse collapse show"
                        aria-labelledby="headingOne"
                        data-bs-parent="#accordionExample"
                      >
                        <div class="accordion-body">零食</div>
                        <div class="accordion-body">泡麵</div>
                        <div class="accordion-body">生鮮食品</div>
                      </div>
                    </div>
                    <div class="accordion-item">
                      <h2 class="accordion-header" id="headingTwo">
                        <button
                          class="accordion-button collapsed"
                          type="button"
                          data-bs-toggle="collapse"
                          data-bs-target="#collapseTwo"
                          aria-expanded="false"
                          aria-controls="collapseTwo"
                        >
                          精品服飾
                        </button>
                      </h2>
                      <div
                        id="collapseTwo"
                        class="accordion-collapse collapse"
                        aria-labelledby="headingTwo"
                        data-bs-parent="#accordionExample"
                      >
                        <div class="accordion-body">全部</div>
                        <div class="accordion-body">男性服飾</div>
                        <div class="accordion-body">女性服飾</div>
                        <div class="accordion-body">嬰幼服飾</div>
                      </div>
                    </div>
                    <div class="accordion-item">
                      <h2 class="accordion-header" id="headingThree">
                        <button
                          class="accordion-button collapsed"
                          type="button"
                          data-bs-toggle="collapse"
                          data-bs-target="#collapseThree"
                          aria-expanded="false"
                          aria-controls="collapseThree"
                        >
                          日常用品
                        </button>
                      </h2>
                      <div
                        id="collapseThree"
                        class="accordion-collapse collapse"
                        aria-labelledby="headingThree"
                        data-bs-parent="#accordionExample"
                      >
                        <div class="accordion-body">洗浴用品</div>
                        <div class="accordion-body">生活小物</div>
                      </div>
                    </div>
                  </div>
                </ul>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </div>
    <button @click="scrollToTop" class="scroll-to-top-btn">
      <i class="fas fa-arrow-up"></i>
    </button>
  </div>
</template>

<style lang="scss" scoped>
.scroll-to-top-btn {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 40px;
  height: 40px;
  border: none;
  border-radius: 50%;
  background-color: #3498db; // 自行調整按鈕背景色
  color: #fff; // 自行調整按鈕文字顏色
  z-index: 99;
  font-size: 20px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.3s;

  &:hover {
    background-color: #2980b9; // 自行調整按鈕hover時的背景色
  }

  i {
    margin-top: 1px;
  }
}
.notification-badge {
  background-color: red;
  color: white;
  border-radius: 50%;
  padding: 4px 8px;
  font-size: 12px;
  position: relative;
  top: -8px;
  left: 4px;
}
.type {
  position: relative;
  top: 15%;
  width: 150px;
  margin-left: -10px;
  border: 0;
}

.btn {
  text-decoration: none;
  color: white;

  font-size: 20pt;
  &:hover {
    background-color: gray;
  }
}

.searchicon {
  font-size: 28pt;
}

.usericon {
  font-size: 20pt;
}
.memberInformation {
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
}

.askUserPage {
  background-color: rgb(92, 92, 92);
  display: flex;
  flex-direction: column;
  border: 0px solid rgb(255, 0, 0);
  color: white;
  padding: 10px;
  height: 20vh;
  width: 100vw;
  .headerfirst {
    display: flex;
    justify-content: space-between;
  }
  .askHeader {
    justify-content: space-around;
    align-items: center;
    display: flex;
    font-size: 16pt;
    padding: 5px;
    border: 0px solid rgb(255, 0, 0);

    .search {
      width: 40vw;
      display: flex;
      justify-content: space-around;
      height: 5vh;
      z-index: 2;

      i {
        font-size: 20pt;
        margin: 0 10px;
      }

      .searchText {
        padding: 10px;
        width: 50vw;
        font-size: 16pt;
      }
    }
  }
}
.Marquee {
  width: 100vw;

  height: 10vh;
  background-color: rgb(48, 48, 48);

  //跑馬燈
  .announcement {
    position: absolute;
    top: 23%;
    right: 100%;
    /* 初始位置在页面右侧外部 */
    background-color: #ff9800;
    /* 公告条背景颜色 */
    color: #fff;
    /* 文字颜色 */
    padding: 10px;
    white-space: nowrap;
    /* 不换行 */
    animation: scrollFromRight 10s linear infinite;
    /* 使用动画效果 */

    p {
      margin: 0;
    }
  }

  @keyframes scrollFromRight {
    0% {
      right: 100%;
    }

    100% {
      right: 0;
    }
  }
}
</style>
