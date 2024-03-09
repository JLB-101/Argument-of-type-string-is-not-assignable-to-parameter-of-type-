# Argument-of-type-string-is-not-assignable-to-parameter-of-type-
here is how to solve
eng: Is the "not assignable to type parameter ever" error in TypeScript.
pt: aqui está como resolver
O erro "não atribuível ao parâmetro de tipo nunca" ocorre no TypeScript?


# error discussion forums: access this link find and learn more about this prisma error 
link: https://github.com/prisma/prisma/issues/20171

# Code: this.$on("beforeExit") doesn't work anymore on 5.0.0 #20171 
import { INestApplication,Injectable, OnModuleInit } from '@nestjs/common';
import { PrismaClient } from '@prisma/client';

@Injectable()
export class PrismaService extends PrismaClient implements OnModuleInit {
  async onModuleInit() {
    await this.$connect();
  }

  // code that cause error  this.$on("beforeExit") doesn't work anymore on 5.0.0 #20171 
  async enableShutdownHooks(app: INestApplication) {
   this.$on('beforeExit', async () => {
    await app.close();
   });
  }
}

#  code: code with error or bug resolved

import { INestApplication,Injectable, OnModuleInit } from '@nestjs/common';
import { PrismaClient } from '@prisma/client';

@Injectable()
export class PrismaService extends PrismaClient implements OnModuleInit {
  async onModuleInit() {
    await this.$connect();
  }

  async enableShutdownHooks(app: INestApplication) {
    process.on('beforeExit', () => {
      app.close();
    });
  }
}

# now test
:npm run start:dev
