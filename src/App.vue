<template>
  <span class="wrapper">
    <nav-bar>
      <li class="side-nav-title side-nav-item">Menu</li>
      <li class="side-nav-item">
        <router-link class="side-nav-link" to="/">
          <i class="mdi mdi-home"></i>
          <span> Início </span>
        </router-link>
      </li>
    </nav-bar>

    <main class="content-page">
      <div class="content">
        <header-vue/>
        <div class="container-fluid">
          <router-view></router-view>
        </div>
      </div>
    </main>
  </span>
</template>

<script>
import NavBar from '@/components/layouts/NavBar'
import HeaderVue from '@/components/layouts/HeaderVue'

var scope = {}

export default {
  name: 'app',
  components: {
    NavBar,
    HeaderVue
  }
}

// -----------------TRELLO API-----------------------

function onAuthorize() {
    updateLoggedIn()

    Trello.members.get("me", function (member) {
        scopeTrelloUser = member

        // Busca as boards do usuário
        Trello.get("members/me/boards", function (boards) {
            $.each(boards, function (ix, board) {
                //Busca cards abertas de cada board do usuário
                Trello.get(`boards/${board.shortLink}/cards/open`, function (cards) {
                    var myCards = []
                    $.each(cards, function (ix, card) {
                        $.each(card.idMembers, function (ix, member) {
                            if (member == scopeTrelloUser.id) {
                                myCards.push(card)
                            }
                        })
                    })
                    board.cards = myCards
                })
            })
            scopeTrelloBoards = boards
            console.log("------FIM-----")
            console.log(scopeTrelloBoards)
        })
    })

}

var updateLoggedIn = function () {
    scopeTrelloIsLoggedIn = Trello.authorized()
}

// scopeTrelloLogout = function () {
//     Trello.deauthorize()
//     updateLoggedIn()
// }

Trello.authorize({
    interactive: false,
    success: onAuthorize
})

// scopeTrelloLogin = function () {
//     Trello.authorize({
//         type: "popup",
//         success: onAuthorize
//     })
// }

        // -----------------TRELLO API END-----------------------
</script>
