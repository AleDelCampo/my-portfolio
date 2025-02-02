<script>
export default {

    name: 'AppFooter',

    data() {
        return {

            Owner: [{
                nome: "Alessandro",
                cognome: "Del Campo"
            }],

            emails: ["alessandrodelcampo01@gmail.com"],

            socials: [
                "fa-google-plus-g",
                "fa-linkedin",
                "fa-github"],

            socialLinks: [
                "mailto:alessandrodelcampo01@gmail.com",
                "https://www.linkedin.com/in/ale-del-campo",
                "https://github.com/AleDelCampo"
            ]
        }
    }
}
</script>

<template>
    <footer class="bg-footer">
        <div class="container py-5">
            <div class="row">
                <div class="col d-flex flex-column align-items-center">
                    <div class="col-title">
                        Owner
                    </div>
                    <div class="components">
                        <ul>
                            <li v-for="member in Owner" :key="member.nome + member.cognome">
                                <div class="name">
                                    {{ member.nome }} {{ member.cognome }}
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="col d-flex flex-column align-items-center">
                    <div class="col-title">
                        Contact
                    </div>
                    <div class="emails">
                        <ul>
                            <li class="fw-bold" v-for="email in emails" :key="email">
                                {{ email }}
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="col d-flex flex-column align-items-center">
                    <div class="col-title">
                        Socials
                    </div>
                    <div id="social-grid">
                        <div v-for="(social, index) in socials" :key="index" class="icon">
                            <a :href="socialLinks[index]" target="_blank" class="social-link">
                                <i class="fa-brands" :class="social"></i>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <hr style="border-top: 4px solid #fd2dfd;">
        <div class="container py-4">
            <h6 class="text-center mb-3">
                I hope you enjoy my works!! If you have any questions please do not hesitate to contact me!!
            </h6>
            <div id="copyright">
                Copyright© 2025, DevHashirama®.
            </div>
        </div>
    </footer>
</template>

<style lang="scss" scoped>
footer {
    color: black;
}

#footer-title {
    font-size: 1.6em;
    font-weight: bold;
    text-align: center;

    margin-bottom: 20px;
}

.col-title {
    font-size: 1.2em;
    font-weight: 600;

    margin-bottom: 10px;
}

ul {
    margin: 0;
    padding: 0;

    display: flex;
    flex-direction: column;
    align-items: center;
    row-gap: 5px;

    font-size: .8em;
    list-style-type: none;
    opacity: .8;
}

.components {

    li {
        display: flex;
        gap: 8px;

        div {
            font-weight: bold;
        }

    }
}

.bg-footer {
    background-color: #f0f3ff;
}

#social-grid {

    max-width: 200px;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;

    .icon {
        display: flex;
        justify-content: center;
        align-items: center;

        width: 50px;
        height: 50px;

        border: 2px solid #fd25fd;

        font-size: 1.3em;

        transition: all .3s ease-in-out;


    }

    .icon:hover {

        background-color: white;

        color: black;

        cursor: pointer;

    }

}

.social-link {
  color: inherit;
  text-decoration: none; 
}

#copyright {
    text-align: center;
    font-weight: bold;
    font-size: .7em;
    opacity: .8;
}
</style>