<script setup>
import { useApplicationStore } from '@/stores/application.js';
const { userData } = useApplicationStore();
</script>

<template>
    <div class="bg-body-tertiary">
        <div class="container">
            <div class="row py-4 px-3">
                <div class="col-12">
                    <div class="mb-4">
                        <h1 class="fs-3"><b>Home</b></h1>
                    </div>
                    <div>
                        <p>
                            Logged in as: <strong>{{ userData.username }}</strong>
                        </p>
                        <div class="about-section">
                            <div class="about-content">
                                <h5 class="about-header">About</h5>
                                <p>Welcome to Aimodosia Online, your gateway to saving lives through the simple act of donating blood.</p>
                                <ul>
                                    <li><strong>Convenience:</strong> We make it easy for you to find nearby donation centers and schedule appointments that fit your busy schedule.</li>
                                    <li><strong>Safety:</strong> Your well-being is our top priority.</li>
                                    <li><strong>Impact:</strong> With each donation, you have the potential to save up to three lives. Your generosity truly matters.</li>
                                    <li><strong>Community:</strong> Join a community of like-minded individuals who share your passion for making a positive impact on the world.</li>
                                </ul>
                                <p>Ready to make a difference? Sign up today, and together, let's save lives, one donation at a time.</p>
                            </div>
                            <div class="about-image">
                                <img src="https://voicetrustmadurai.org/wp-content/uploads/2022/03/Blood-Donation-1.jpg" alt="Blood Donation" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
.about-section {
    display: flex;
    align-items: center;
}

.about-content {
    flex: 1;
    margin-right: 20px;
}

.about-header {
    border-bottom: 2px solid #333;
    display: inline-block;
    padding-bottom: 2px;
    margin-bottom: 10px;
}

.about-image {
    flex: 1;
}

.about-image img {
    max-width: 100%;
    height: auto;
    border-radius: 8px;
}
</style>