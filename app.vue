<script>
const authState = this.isStoreOpen ? 'Close store' : 'Open store'
</script>

<template>
  <div>
    <va-navbar color="dark" v-if="authState === 'signedin'">
      <template #left>
        <va-navbar-item class="mr-4">
          <div>Barista</div>
        </va-navbar-item>
      </template>
      <template #center>
        <va-navbar-item class="mr-4">
          <va-button :rounded="false" :loading="isStoreChangingState" color="info" @click="storeSwitchChange" >
            {{ getStoreStateButtonLabel }}
          </va-button>
        </va-navbar-item>
        <va-navbar-item>
          <va-switch color="success" label="left" left-label v-model="robotEnabled" @update:model-value="toggleRobot" class="ml-4" >
            Robot
          </va-switch>
        </va-navbar-item>
        <va-navbar-item class="mr-4">
          <va-slider v-if="robotEnabled" style="min-width: 150px;" label="Robot speed" v-model="robotSpeed" color="success"/>
        </va-navbar-item>
        <va-navbar-item class="mr-4" v-show="!isEditingPrinter">
          <va-button :rounded="false" color="info" @click="printerChange" >
            {{ getPrinterButtonLabel }}
          </va-button>
        </va-navbar-item>
        <!-- Edit printer IP -->
        <va-navbar-item v-show="isEditingPrinter">
          <va-input
            v-model="printerIPaddress"
            placeholder="Printer IP address"
          />
        </va-navbar-item>
        <va-navbar-item class="mr-4" v-show="isEditingPrinter">
          <va-button :rounded="false" color="info" @click="printerSaveChange" >
            Save
          </va-button>
        </va-navbar-item>

      </template>
      <template #right>
        <va-navbar-item>
          <va-button color="primary" :rounded="false"  @click="signOut">Sign out</va-button>
        </va-navbar-item>
      </template>
    </va-navbar>

    <!-- Only show if logged out -->
    <div v-if="authState != 'signedin'">
      <Authentication/>
    </div>
    <!-- Only show if logged in -->
    <div v-if="authState === 'signedin'">
      <OrderSelector />
    </div>
    <IoT />
    <!-- <Printing /> -->
  </div>
</template>