<template>
  <div class="container-fluid">
    <div class="contact">
      <h1>Contact</h1>
      <div class="text">
        <h2 class="h2-text">Qui sommes-nous ?</h2>
        <p>
          <span>« Live Events »</span> est une entreprise d’organisation et de
          promotion de spectacles basée sur Paris et créée en 2005. Elle compte
          aujourd’hui une centaine d’employés.
        </p>
      </div>
      <div class="presentation">
        <!-- <h2 class="text">Axel Gonon</h2> -->
        <!-- <img class="image" src="../assets/img/axel.jpg" alt="axel"/> -->
        <div v-for="(contact, index) in info" :key="index">
          <img class="image" :src="contact.picture" />
          <p class="name-presentation">{{ contact.name }}</p>
          <p class="content-presentation">{{ contact.job }}</p>
          <p class="punch-presentation">{{ contact.description }}</p>
        </div>
      </div>

      <div id="form_contact">
        <form class="vue-form" @submit.prevent="submit">
          <div class="error-message">
            <p v-show="!email.valid">Oh, please enter a valid email address.</p>
          </div>

          <fieldset>
            <legend>
              Pour toute demande veuillez-nous contacter via ce formulaire de
              contact :
            </legend>
            <div>
              <label class="label" for="name">Name</label>
              <input
                type="text"
                name="name"
                id="name"
                required=""
                v-model="name"
              />
            </div>
            <div>
              <label class="label" for="email">Email</label>
              <input
                type="email"
                name="email"
                id="email"
                required=""
                :class="{ email, error: !email.valid }"
                v-model="email.value"
              />
            </div>
            <div>
              <h4>Le sujet de ma demande :</h4>
              <p class="select">
                <select class="budget">
                  <option value="0">Je veux être bénévole</option>
                  <option value="1">J'ai perdu quelques choses</option>
                  <option value="2">J'ai une demande</option>
                  <option value="3">Je désire être partenaire</option>
                </select>
              </p>
            </div>

            <div>
              <label class="label" for="textarea">Ma demande</label>
              <textarea
                class="message"
                name="textarea"
                id="textarea"
                required=""
                v-model="message.text"
                :maxlength="message.maxlength"
              ></textarea>
              <span class="counter"
                >{{ message.text.length }} / {{ message.maxlength }}</span
              >
            </div>
            <div>
              <input type="submit" class="big-btn" value="Envoyer" />
            </div>
          </fieldset>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      info: null,
      name: "John Doe",
      email: {
        value: "jo@hnd.oe",
        valid: true,
      },

      message: {
        text: `Bonjour,\n...`,
        maxlength: 999,
      },
      submitted: false,
    };
  },

  mounted() {
    axios
      .get("http://localhost:8000/api/contacts")
      .then((response) => (this.info = response.data))
      .catch((error) => console.log(error));
  },

  methods: {
    // submit form handler
    submit: function() {
      this.submitted = true;
    },
    // validate by type and value
    validate: function(type, value) {
      if (type === "email") {
        this.email.valid = this.isEmail(value) ? true : false;
      }
    },
    // check for valid email adress
    isEmail: function(value) {
      return emailRegExp.test(value);
    },
  },
  watch: {
    // watching nested property
    "email.value": function(value) {
      this.validate("email", value);
    },
  },
};
</script>

<style lang="scss">
.contact {
  .image {
    margin: 13vh 6em 0;
    width: 100px;
    height: 100px;
    clip-path: ellipse(50% 50%);
  }

  .text {
    span {
      color: var(--orange);
      font-size: 1.2rem;
      font-weight: 700;
    }
    padding: 10vw 10vw 3vw 10vw;
    h2 {
      text-align: center;
      margin-bottom: 5vh;
    }
  }

  .presentation {
    display: flex;
    align-items: center;
    flex-flow: row wrap;
    justify-content: space-between;
    // max-width: 700px;
    margin-left: auto;
    margin-right: auto;
    text-align: center;

    & div {
      margin: auto;
    }
  }

  .name-presentation {
    text-align: center;
    margin-top: 3vh;
    font-size: 1.25rem;
    font-weight: 700;
    margin-bottom: 0rem;
  }

  .content-presentation {
    text-align: center;
    font-style: italic;
  }

  .punch-presentation {
    text-align: center;
    font-style: italic;
    font-weight: bold;
  }

  #form_contact {
    margin: auto;
    width: 700px;

    *,
    *::after,
    *::before {
      box-sizing: border-box;
    }
    color: #fff;
    background: #fff;

    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
      Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", Helvetica, Arial,
      sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

    .center {
      display: flex;
      justify-content: center;
      align-items: center;
    }

    a {
      color: #2c3e50;
      text-decoration: none;
    }

    .vue-form {
      font-size: 16px;
      //width: 500px;
      padding: 15px 30px;
      //border-radius: 4px;
      margin: 50px auto;
      // width: 500px;
      background-color: #fff;
      //box-shadow: 0 4px 6px 0 rgba(0, 0, 0, 0.3);
    }
    .vue-form fieldset {
      margin: 24px 0 0 0;
    }
    .vue-form legend {
      padding-bottom: 10px;
      border-bottom: 1px solid #ecf0f1;
      color: var(--orange);
      font-size: 1.25rem;
      font-weight: 700;
    }
    .vue-form div {
      position: relative;
      margin: 20px 0;
    }
    .vue-form h4,
    .vue-form .label {
      color: #94aab0;
      margin-bottom: 10px;
    }
    .vue-form .label {
      display: block;
    }
    .vue-form input,
    .vue-form textarea,
    .vue-form select,
    .vue-form label {
      color: #2b3e51;
    }
    .vue-form input[type="text"],
    .vue-form input[type="email"],
    .vue-form textarea,
    .vue-form select,
    .vue-form legend {
      display: block;
      width: 100%;
      appearance: none;
    }
    .vue-form input[type="text"],
    .vue-form input[type="email"],
    .vue-form textarea,
    .vue-form select {
      padding: 4px 12px;
      border: 1px solid #cfd9db;
      background-color: #ffffff;
      border-radius: 0.25em;
      box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.08);
    }
    .vue-form input[type="text"]:focus,
    .vue-form input[type="email"]:focus,
    .vue-form textarea:focus,
    .vue-form select:focus {
      outline: none;
      border-color: #2c3e50;
      box-shadow: 0 0 5px rgba(44, 151, 222, 0.2);
    }
    .vue-form .select {
      position: relative;
    }
    .vue-form .select::after {
      content: "";
      position: absolute;
      z-index: 1;
      right: 16px;
      top: 50%;
      margin-top: -8px;
      display: block;
      width: 16px;
      height: 16px;
      background: url("data:image/svg+xml;charset=utf-8,%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22utf-8%22%3F%3E%0D%0A%3C%21DOCTYPE%20svg%20PUBLIC%20%22-%2F%2FW3C%2F%2FDTD%20SVG%201.1%2F%2FEN%22%20%22http%3A%2F%2Fwww.w3.org%2FGraphics%2FSVG%2F1.1%2FDTD%2Fsvg11.dtd%22%3E%0D%0A%3Csvg%20version%3D%221.1%22%20id%3D%22Layer_1%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20x%3D%220px%22%20y%3D%220px%22%0D%0A%09%20width%3D%2216px%22%20height%3D%2216px%22%20viewBox%3D%220%200%2016%2016%22%20enable-background%3D%22new%200%200%2016%2016%22%20xml%3Aspace%3D%22preserve%22%3E%0D%0A%3Cg%3E%0D%0A%09%3Cpolygon%20fill%3D%22%232c3e50%22%20points%3D%220.9%2C5.5%203.1%2C3.4%208%2C8.3%2012.9%2C3.4%2015.1%2C5.5%208%2C12.6%20%09%22%2F%3E%0D%0A%3C%2Fg%3E%0D%0A%3C%2Fsvg%3E")
        no-repeat center center;
      pointer-events: none;
    }
    .vue-form select {
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
      cursor: pointer;
    }
    .vue-form select::-ms-expand {
      display: none;
    }
    .vue-form .vue-form-list {
      margin-top: 16px;
    }
    .vue-form .vue-form-list::after {
      clear: both;
      content: "";
      display: table;
    }

    .vue-form textarea {
      min-height: 120px;
      resize: vertical;
      overflow: auto;
    }
    .vue-form input[type="submit"] {
      float: right;
      padding: 8px 60px 10px;
    }
    .no-touch .vue-form input[type="submit"]:hover {
      background: #42a2e1;
    }
    .vue-form input[type="submit"]:focus {
      outline: none;
      background-color: var(--pink);
    }
    .vue-form input[type="submit"]:active {
      transform: scale(0.9);
    }
    .vue-form .error-message {
      height: 35px;
      margin: 0px;
    }
    .vue-form .error-message p {
      background: #e94b35;
      color: #ffffff;
      font-size: 1.4rem;
      text-align: center;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      border-radius: 0.25em;
      padding: 16px;
    }
    .vue-form .error {
      border-color: #e94b35 !important;
    }
    .vue-form .counter {
      background-color: #ecf0f1;
      position: absolute;
      right: 0px;
      top: 0px;
      font-size: 10px;
      padding: 4px;
    }

    .debug {
      border-radius: 4px;
      margin: 50px auto;
      //width: 500px;
      background-color: #000;
      padding: 50px;
      background: rgba(0, 0, 0, 0.8);
      box-shadow: 0 4px 6px 0 rgba(0, 0, 0, 0.3);
    }

    .debug pre {
      color: #ffffff;
      font-size: 18px;
      line-height: 30px;
      font-family: "Source Code Pro", monospace;
      font-weight: 300;
      white-space: pre-wrap;
    }

    @-webkit-keyframes cd-bounce {
      0%,
      100% {
        -webkit-transform: scale(1);
      }
      50% {
        -webkit-transform: scale(0.8);
      }
    }
    @-moz-keyframes cd-bounce {
      0%,
      100% {
        -moz-transform: scale(1);
      }
      50% {
        -moz-transform: scale(0.8);
      }
    }
    @keyframes cd-bounce {
      0%,
      100% {
        transform: scale(1);
      }
      50% {
        transform: scale(0.8);
      }
    }
  }
}
</style>
