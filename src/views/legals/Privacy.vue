<template>
  <the-disclaimer v-show="isVisible" @close="close">
    <template v-slot:header>
      <h2>Privacy Policy</h2>
    </template>
    <template #body>
      <ul class="custom-bullet">
        <br />

        <li>
          At MyLlama, we value the privacy of our visitors. This Privacy Policy
          explains the types of information we collect and how we use it. If you
          have any additional questions or need more information, please don't
          hesitate to contact us. This Privacy Policy applies only to our online
          activities and is valid for visitors to our website with respect to
          the information they share and/or collect on MyLlama. It does not
          apply to any offline information or information collected through
          other channels. By using our website, you consent to our Privacy
          Policy and agree to its terms.
        </li>
        <br />
        <li>
          <span>Information We Collect:</span> When you use our website, you may
          be asked to provide certain personal information. The reasons for
          collecting this information will be made clear to you at the time of
          collection. If you contact us directly, we may receive additional
          information such as your name, email address, phone number, the
          contents of your message, and any other information you choose to
          provide. When you register for an account, we may ask for your contact
          information, including items such as your name, company name, address,
          email address, and telephone number.
        </li>
        <br />
        <li>
          <span>How We Use Your Information:</span> We use the information we
          collect for various purposes, including providing, operating, and
          maintaining our website, improving and personalizing user experiences,
          understanding and analyzing website usage, developing new products and
          services, communicating with users, and sending updates and
          promotional information. We may also use your information to prevent
          fraud.
        </li>
        <br />
        <li>
          <span>Log Files: </span>
          MyLlama follows standard procedures for using log files. These files
          log visitors when they visit websites. The information collected may
          include internet protocol (IP) addresses, browser type, Internet
          Service Provider (ISP), date and time stamps, referring/exit pages,
          and possibly the number of clicks. This information is used for
          analyzing trends, administering the site, tracking user movement, and
          gathering demographic information. The collected information is not
          linked to any personally identifiable information.
        </li>
        <br />

        <li>
          <span> Cookies and Web Beacons:</span>
          Like many other websites, MyLlama uses cookies to enhance user
          experiences and personalize web page content. Cookies store
          information about visitors' preferences and the pages they access or
          visit. This information is used to optimize the user experience by
          customizing content based on the visitor's browser type and other
          information.
        </li>
        <br />
        <li>
          <span> Advertising Partners Privacy Policies:</span>
          Please consult the respective Privacy Policies of our advertising
          partners for detailed information. Third-party ad servers or ad
          networks may use technologies like cookies, JavaScript, or web beacons
          to personalize advertising content and measure the effectiveness of
          their campaigns. MyLlama has no access to or control over these
          cookies used by third-party advertisers.
        </li>
        <br />

        <br />
        <li>
          <span> Third-Party Privacy Policies:</span>
          MyLlama's Privacy Policy does not apply to other advertisers or
          websites. We recommend reviewing the Privacy Policies of third-party
          ad servers for detailed information on their practices and
          instructions on how to opt out of certain options. You can also
          disable cookies through your browser settings. Visit your browser's
          website for more information on managing cookies.
        </li>
        <br />

        <br />
        <li>
          <span>
            CCPA Privacy Rights (Do Not Sell My Personal Information):</span
          >
          Under the CCPA, California consumers have the right to request
          disclosure of the categories and specific pieces of personal data
          collected by a business, request deletion of personal data, and
          request a business that sells personal data not to sell their personal
          data. If you would like to exercise any of these rights, please
          contact us. We have one month to respond to your request.
        </li>
        <br />

        <br />
        <li>
          <span> GDPR Data Protection Rights:</span>
          You have the right to access, correct, erase, restrict processing,
          object to processing, and request data portability. If you would like
          to exercise any of these rights, please contact us. We have one month
          to respond to your request.
        </li>
        <br />

        <br />
        <li>
          <span>Children's Information:</span>
          Protecting children's privacy online is important to us. We encourage
          parents and guardians to monitor and guide their children's online
          activities. MyLlama does not knowingly collect personal identifiable
          information from children under the age of 13. If you believe that
          your child has provided personal information on our website, please
          contact us immediately, and we will make our best efforts to promptly
          remove such information from our records.
        </li>
        <br />

        <br />
        <li>
          <span>Children's Information:</span>
          Protecting children's privacy online is important to us. We encourage
          parents and guardians to monitor and guide their children's online
          activities. MyLlama does not knowingly collect personal identifiable
          information from children under the age of 13. If you believe that
          your child has provided personal information on our website, please
          contact us immediately, and we will make our best efforts to promptly
          remove such information from our records.
        </li>
        <br />
      </ul>
      <br />
    </template>
  </the-disclaimer>
</template>

<script>
import TheDisclaimer from "./TheDisclaimer.vue";
export default {
  components: {
    TheDisclaimer,
  },

  data() {
    return {
      isVisible: false,
    };
  },
  methods: {
    show() {
      this.isVisible = true;
    },
    close() {
      this.isVisible = false;
    },
  },
};
</script>

<style scoped>
span {
  font-weight: bold;
}
.custom-bullet {
  text-align: justify;
}
</style>