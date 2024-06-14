<template>
  <div class="domain-checker">
    <el-card class="box-card">
      <h1>Domain Checker</h1>
      <el-form @submit.prevent="checkDomain" inline>
        <el-form-item>
          <el-input v-model="domain" placeholder="Enter domain"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="checkDomain">Check Domain</el-button>
        </el-form-item>
      </el-form>
      <el-card v-if="domainDetails" class="result-card">
        <template #header>
          <h2>Domain Information</h2>
        </template>
        <div class="result-content">
          <p><strong>Domain:</strong> {{ domainDetails.domain }}</p>
          <p><strong>Top Level Domain (TLD):</strong> {{ domainDetails.tld }}</p>
          <p><strong>Valid:</strong> {{ domainDetails.valid ? 'Yes' : 'No' }}</p>
          <p><strong>Available:</strong> {{ domainDetails.available ? 'Yes' : 'No' }}</p>
          <p><strong>Registrar:</strong> {{ domainDetails.registrar }}</p>
          <p><strong>Created At:</strong> {{ domainDetails.created_at }}</p>
          <p><strong>Updated At:</strong> {{ domainDetails.updated_at }}</p>
          <p><strong>Expires At:</strong> {{ domainDetails.expires_at }}</p>
          <p><strong>Whois Server:</strong> <a :href="domainDetails.whois" target="_blank">{{ domainDetails.whois }}</a></p>
        </div>
      </el-card>
      <el-alert v-if="error" type="error" :closable="false" show-icon>
        {{ error }}
      </el-alert>
    </el-card>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';

export default defineComponent({
  data() {
    return {
      domain: '',
      domainDetails: null as any | null,
      error: null as string | null
    };
  },
  methods: {
    async checkDomain() {
      const options = {
        method: 'GET',
        url: 'https://domain-checker7.p.rapidapi.com/whois',
        params: {
          domain: this.domain
        },
        headers: {
          'x-rapidapi-key': 'faa271f72fmshfe9df8831015cddp121d98jsn308069e51507',
          'x-rapidapi-host': 'domain-checker7.p.rapidapi.com'
        }
      };

      try {
        const response = await axios.request(options);
        this.domainDetails = response.data;
        this.error = null;
      } catch (error) {
        this.error = 'Error fetching data';
        console.error(error);
      }
    }
  }
});
</script>

<style scoped>
.domain-checker {
  max-width: 600px;
  margin: 20px auto;
  padding: 20px;
}

.box-card {
  margin-top: 20px;
}

.result-card {
  margin-top: 20px;
}

.result-content {
  padding: 20px;
}

h1, h2 {
  text-align: center;
}
</style>
