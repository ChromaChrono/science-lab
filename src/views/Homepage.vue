<template>
  <the-hero></the-hero>
  <the-about @aboutRef="aboutRef = $event" @cardsRef="cardsRef = $event" @outroRef="outroRef = $event"
    :animateAbout="animateAbout" :animateCards="animateCards" :animateOutro="animateOutro"></the-about>
  <the-portfolio :animatePortfolio="animatePortfolio" @portfolioRef="portfolioRef = $event"></the-portfolio>
  <the-contact-form @contactRef="contactRef = $event" :animateContact="animateContact"></the-contact-form>
</template>
<script>
import TheHero from "../components/view-specific/homepage/TheHero.vue";
import TheAbout from "../components/view-specific/homepage/TheAbout.vue";
import ThePortfolio from "../components/view-specific/homepage/ThePortfolio.vue";
import TheContactForm from "../components/view-specific/homepage/TheContactForm.vue";
export default {
  data() {
    return {
      aboutRef: null,
      outroRef: null,
      cardsRef: null,
      contactRef: null,
      portfolioRef: null,
      animateAbout: false,
      animateOutro: false,
      animateCards: false,
      animatePortfolio: false,
      animateContact: false,
    };
  },
  components: {
    TheHero,
    TheAbout,
    ThePortfolio,
    TheContactForm,
  },
  mounted() {
    if (window.screenX < 1000) {
      this.animate = true;
    }

    let options = {
      root: null,
      threshold: 0.2,
      rootMargin: "0px",
    };

    const observer = new IntersectionObserver((entries, observer) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) {
          return;
        }
        if (entry.target === this.aboutRef) {
          this.animateAbout = true;
          observer.unobserve(entry.target);
        } else if (entry.target === this.cardsRef) {
          this.animateCards = true;
          observer.unobserve(entry.target);
        } else if (entry.target === this.outroRef) {
          this.animateOutro = true;
          observer.unobserve(entry.target);
        } else if (
          entry.target === this.portfolioRef &&
          !this.animatePortfolio
        ) {
          this.animatePortfolio = true;
          observer.unobserve(entry.target);
        } else if (entry.target === this.contactRef) {
          this.animateContact = true;
          observer.unobserve(entry.target);
        }
      });
    }, options);

    observer.observe(this.aboutRef);
    observer.observe(this.outroRef);
    observer.observe(this.cardsRef);
    observer.observe(this.portfolioRef);
    observer.observe(this.contactRef);
  },
};
</script>
<style lang="scss"></style>
